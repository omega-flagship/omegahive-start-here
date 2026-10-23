# Primer: truth values, NAL and PLN

## What it is
- **A truth value** here is `(stv f c)`. **f** (frequency, or strength in PLN) is how often the statement held in the evidence seen. **c** (confidence) is how much evidence there is, on a 0 to 1 scale that never reaches 1.
- **NAL** (Non-Axiomatic Logic) is the logic of NARS. Its rules derive new statements from two premises and compute the conclusion's truth value. Statements look like `(--> robin bird)`, "robin is a kind of bird".
- **PLN** (Probabilistic Logic Networks) is OpenCog's probabilistic logic. Statements look like `(Inheritance A B)`.
- **NARS** is the reasoning system NAL comes from. PeTTa ships its own NARS library, which minds also load.

## Why it is used here
Every native mind loads `lib_nal`, `lib_pln` and PeTTa's `lib_nars` ([`omegahive/lib_omegaclaw_core.metta:12-14`](https://github.com/PhysixSNET/omegahive/blob/main/lib_omegaclaw_core.metta#L12-L14)). The mind's model can call them as skills (`nal-step`, `pln-step`, `nars-query`, `nars-derive`). The swarm commons uses the NAL revision rule to merge members' beliefs. Apps may label uncertainty with `{"method": "nal", "f", "c"}` ([`omegahive/hive/PROGRAMS.md:123-128`](https://github.com/PhysixSNET/omegahive/blob/main/hive/PROGRAMS.md#L123-L128)).

## The minimum you must know
- **Confidence and evidence weight convert both ways:** w = c / (1 − c), and c = w / (w + 1) ([`omegahive/lib_nal.metta:2-6`](https://github.com/PhysixSNET/omegahive/blob/main/lib_nal.metta#L2-L6)). So c = 0.9 is evidence weight 9.
- **Revision** merges two beliefs about the *same* statement by adding their evidence weights ([`omegahive/lib_nal.metta:92-99`](https://github.com/PhysixSNET/omegahive/blob/main/lib_nal.metta#L92-L99)). More independent evidence, more confidence.
- **Expectation** turns `(stv f c)` into one number: c × (f − 0.5) + 0.5 ([`omegahive/lib_nal.metta:101-102`](https://github.com/PhysixSNET/omegahive/blob/main/lib_nal.metta#L101-L102)). Low confidence pulls it toward 0.5.
- **Revision is only honest with disjoint evidence.** The commons carries **evidence stamps** (lists of ids such as `(ev omega-a 1)`) and revises only when stamps do not overlap; otherwise it keeps the higher-confidence belief ([`omegahive/hive/spaces/lib_hive.metta:6-9`](https://github.com/PhysixSNET/omegahive/blob/main/hive/spaces/lib_hive.metta#L6-L9)). The skills carry no stamps.
- **Reasoning is not automatic in this build.** The model decides when to call a skill. Automatic reasoning from the loop is deliberately not wired ([`omegahive/STATUS.md:49`](https://github.com/PhysixSNET/omegahive/blob/main/STATUS.md#L49)).

## A tiny example
NAL revision and deduction ([`omegahive/lib_nal.metta:92-99, 108-110`](https://github.com/PhysixSNET/omegahive/blob/main/lib_nal.metta#L92-L99)):

```metta
(= (Truth_Revision (stv $f1 $c1) (stv $f2 $c2))
   (let* (($w1 (Truth_c2w $c1)) ($w2 (Truth_c2w $c2)) ($w (+ $w1 $w2))
          ($f (/ (+ (* $w1 $f1) (* $w2 $f2)) $w)) ($c (Truth_w2c $w)))
          (stv (min 1.00 $f) (min 0.99 (max (max $c $c1) $c2)))))

(= (|-nal ($T $T1) ($T $T2)) ($T (Truth_Revision $T1 $T2)))
(= (|-nal ((--> $a $b) $T1) ((--> $b $c) $T2)) ((--> $a $c) (Truth_Deduction $T1 $T2)))
```

(The revision rule is reflowed here; the source spreads it over eight lines.) The first rule says: two premises with the same statement `$T` revise. The second: from a→b and b→c, derive a→c by deduction. The commons runs a copy of the same revision rule, and a smoke test checks the two agree ([`omegahive/tests/hive_lib_smoke.metta:30-34`](https://github.com/PhysixSNET/omegahive/blob/main/tests/hive_lib_smoke.metta#L30-L34)).

## Common pitfalls
Read [`omegahive/docs/reasoning-deviations.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reasoning-deviations.md) before you trust a number. The main ones:
- **Duplicates in a running mind.** Loading both `lib_nal` and PeTTa's `lib_nars` defines `|-` and every `Truth_*` helper twice, so `nal-step` returns raw duplicates ([`omegahive/docs/reasoning-deviations.md:33-39`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reasoning-deviations.md#L33-L39)).
- **Self-revision inflates confidence on the skill path,** because it has no stamps ([`omegahive/docs/reasoning-deviations.md:40-43`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reasoning-deviations.md#L40-L43)).
- **Caps differ.** NAL and the commons cap revised c at 0.99; PLN caps at 1.0; at c = 1, NAL raises a division error ([`omegahive/docs/reasoning-deviations.md:44-48`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reasoning-deviations.md#L44-L48)).
- **Five revision rules exist** across the code, with different caps ([`omegahive/docs/reasoning-deviations.md:49-52`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reasoning-deviations.md#L49-L52)).
- **PLN uses a constant prior** of ⟨0.1, 0.9⟩ for every term ([`omegahive/lib_pln.metta:49`](https://github.com/PhysixSNET/omegahive/blob/main/lib_pln.metta#L49)), plus several other differences from the references ([`omegahive/docs/reasoning-deviations.md:53-63`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reasoning-deviations.md#L53-L63)).
- **Do not change truth semantics on your own.** The libraries stay unchanged by the owner's ruling; any change goes to the domain author before merge ([`omegahive/docs/reasoning-deviations.md:7-9`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reasoning-deviations.md#L7-L9)).
- **Consensus is not proof.** Check a formal claim against the governing rule and its reference, not against reviewers' agreement.

## Upstream
- **NAL:** the *NAL Specification* (Wang), the reference the audit used ([`omegahive/docs/reasoning-deviations.md:11`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reasoning-deviations.md#L11)).
- **ONA,** OpenNARS for Applications, whose `Truth.c` is the NAL reference here.
- **PLN:** the PLN book, OpenCog's PLN rules, and <https://github.com/trueagi-io/PLN> (the audit used commit `4405956`).
- **NARS in PeTTa:** PeTTa's bundled `lib_nars`, in <https://github.com/trueagi-io/PeTTa>.

## Read next
- [`omegahive-schematics/04-knowledge/03-reasoning.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/03-reasoning.md): how reasoning is reached today, and what is held.
- [`omegahive-schematics/04-knowledge/02-beliefs-sharing.md`](https://github.com/PhysixSNET/omegahive-schematics/blob/main/04-knowledge/02-beliefs-sharing.md): stamps and revision in the commons.
- [`omegahive/docs/reference-lib-nal.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reference-lib-nal.md) and [`omegahive/docs/reference-lib-pln.md`](https://github.com/PhysixSNET/omegahive/blob/main/docs/reference-lib-pln.md): the reference pages.
