# Topic 11: Troubleshooting & Case Studies

## Overview
Diagnosing signal loss, system instability, unexpected biological behaviors, and structured problem-solving for real-world biocomputing software engineering scenarios.

---

### Q1: A previously stable closed-loop biocomputing system, running well for several days, suddenly shows dramatically degraded spike detection performance — spike counts drop to near zero on most channels, the closed-loop stimulation behavior becomes erratic, and the biological substrate appears quiescent. Walk through your systematic troubleshooting approach.

**A:**
**Systematic troubleshooting — ordered from most likely/quickest-to-check to more involved:**

1. **First: check hardware signals and basic acquisition path before assuming biological explanation:** Verify the raw voltage signal at the amplifier output is present and within expected range (ruling out a complete electrical connection failure — disconnected cable, power failure to acquisition hardware, amplifier malfunction); check that the ADC is receiving and digitizing the signal; verify data is successfully reaching the software processing pipeline. A complete loss of signal at any hardware stage produces exactly the symptom of "no detected spikes" regardless of biological substrate state — and hardware failure is often more common and quicker to resolve than a genuine biological catastrophe.

2. **Second: check life-support system status if applicable:** For ex vivo substrates, verify temperature, CO₂/O₂, media perfusion, and other life-support parameters are within normal range — a life-support failure would produce exactly the "quiescent substrate" symptom through biological mechanism (cell distress/death) rather than an artifact.

3. **Third: check recording amplifier saturation:** Large, sustained DC offset or amplifier saturation (perhaps from a broken electrode creating a DC short, or a chemical event in the media changing the electrode-media potential) can push amplifiers into saturation, producing a flat, apparently quiescent signal that is actually a hardware artifact rather than genuine biological silence — check raw signal baseline level for saturation indicators.

4. **Fourth: assess whether the quiescence is genuinely biological:** If hardware and life-support checks are normal and the raw signal shows non-saturated, physiologically-plausible amplitude signal with simply no spiking activity (not zero-amplitude or DC-saturated signal), then genuine biological quiescence (the network has entered a quiescent state, or suffered biological damage causing genuine reduced activity) becomes the more plausible explanation — review the stimulation history logs (was there a recent unusual stimulation event that could have caused excitotoxic damage?) and biological observation records for any signs of substrate health concerns.

5. **Throughout: maintain detailed incident log:** Document all checks performed, results, and timeline, both for immediate diagnostic efficiency and for post-incident analysis that may inform future system design improvements.

**Key principle:** As with troubleshooting across this repository series, systematic progression from mundane/technical explanations (hardware failure, connection issues) to more fundamental/biological explanations — resisting the temptation to immediately assume the most scientifically interesting or challenging explanation (biological catastrophe) before ruling out more common, simpler explanations.

### Q2: Case study — A biocomputing experiment designed to test whether an organoid can learn to respond differentially to two distinct stimulus patterns shows no evidence of differential response after 5 days of training stimulation. How do you distinguish between a software/methodology failure and a genuine negative biological result?

**A:**
**Systematic diagnostic approach:**

1. **Verify the stimulation delivery log confirms intended stimulation was actually delivered correctly:** Confirm from hardware-level stimulation delivery confirmation logs (not just software-level command logs) that the two intended stimulus patterns were delivered with the intended parameters, timing, and electrode targeting — a software bug causing both "conditions" to deliver identical stimulation, or delivering stimulation to wrong electrodes, would produce apparent failure to discriminate that isn't a genuine biological negative result.

2. **Verify the recording and decoding pipeline is sensitive enough to detect differential responses if they existed:** Test the discriminability of the decoding pipeline using known-different stimulation responses (e.g., deliver a clearly different "test" stimulation pattern not used in training and confirm the decoder detects it as different from baseline) — if the decoder can't discriminate even large, obvious differences in evoked activity, the problem is in the decoding/analysis pipeline sensitivity rather than the biological substrate's failure to learn.

3. **Check for confounds in the experimental design — was the biological substrate in a suitable state for learning throughout the training period?** Review the longitudinal biological state logs for any evidence of life-support instability, recording quality degradation, or anomalous biological states during the training period that might have disrupted the intended learning opportunity — a learning experiment conducted during periods of biological substrate stress may produce null results through substrate health problems rather than genuine absence of learning capacity.

4. **If software/methodology issues are ruled out, apply statistical rigor to assess whether this is a genuine negative result versus insufficient power:** Consider whether the experiment had adequate statistical power to detect a biologically realistic effect size — it's possible that a genuine but small differential response exists but wasn't detectable with the experiment's duration, sample size (number of recorded units), or chosen analysis approach, making this potentially a "negative result due to insufficient sensitivity" rather than either a genuine null biological result or a software failure.

5. **Distinguish a "this specific experiment design didn't work" finding from a "organoids can't learn" conclusion:** Even if all the above checks confirm a genuine negative result, interpret it appropriately narrowly — this specific stimulus pair, training duration, stimulation parameter set, and organoid batch didn't produce detectable differential response, which is informative but doesn't support the much stronger (and unsupported) conclusion that organoid learning is impossible.

### Q3–Q13: (Representative additional topics)
- Diagnosing intermittent spike detection failures traced to subtle real-time scheduling jitter
- Troubleshooting stimulation artifact subtraction failures producing false spike detections
- Root-causing unexpected cross-channel correlation patterns suggesting electrode electrical short
- Investigating closed-loop system oscillation (stimulation → response → stimulation feedback loop becoming unstable)
- Diagnosing systematic bias in spike sorting (certain unit types consistently mis-sorted)
- Troubleshooting data integrity failures in long-duration recording sessions
- Investigating unexpected biological network state transitions during experiments
- Root-causing safety system false-positive triggers interrupting otherwise normal experiments
- Diagnosing latency regression following software update to a previously-validated real-time pipeline
- Handling safety-relevant unexpected biological events and the required incident response process

---

## Summary
Rigorous troubleshooting in biocomputing systems requires systematically distinguishing hardware/connection failures, software bugs and analysis pipeline limitations, life-support and biological health issues, and genuine biological findings — applying the same disciplined, evidence-ordered diagnostic approach emphasized throughout this repository series before concluding that a genuinely novel or scientifically interesting explanation (biological catastrophe, genuine learning failure) accounts for an observed anomaly.
