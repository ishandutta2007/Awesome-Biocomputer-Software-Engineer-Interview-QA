# Topic 10: Cross-Functional Collaboration

## Overview
Working effectively with neuroscientists/biologists, hardware/electronics engineers, and computational neuroscientists as a Biocomputer Software Engineer.

---

### Q1: How do you build effective collaborative relationships with neuroscientists and biologists, given the genuine disciplinary gulf between software engineering and biology, and the particular importance of this collaboration for building software that correctly models biological reality?

**A:**
**Trust-building and collaboration approach:**
1. **Invest genuinely in biological domain literacy, treating it as a core professional competency not a peripheral "nice to have":** A Biocomputer Software Engineer who understands only the signal/data aspects of the biological computing substrate — treating the biology as a black box producing signals — will systematically build software that mismodels biologically-important realities (e.g., designing a spike sorting system without understanding why waveform shapes drift, or building a closed-loop control system without understanding the timescales of the relevant biological plasticity mechanisms being targeted). Genuine biological domain literacy, developed through deliberate study and close collaboration with biology colleagues, directly improves software design quality in ways that aren't achievable without this investment.

2. **Approach biology collaborators as the domain authority on biological behavior, neither dismissing biological nuance as "implementation detail" nor overwhelming biologists with software engineering jargon they don't need to engage with at full depth:** The most productive collaborations establish a genuine bidirectional technical dialogue where biology and software engineering considerations genuinely inform each other — rather than either a one-directional "biology generates requirements, software implements them" model (which misses the genuine iterative co-design value of close collaboration) or a collaboration where different disciplines talk past each other in untranslated disciplinary jargon.

3. **Make software systems' biological assumptions explicit and visible to biology collaborators for expert review:** Since software systems interfacing with biological substrates necessarily embody specific assumptions about biological behavior (in spike sorting templates, in decoder model assumptions, in safety threshold choices), making these biological assumptions explicit — in code documentation, in configuration parameters, in analysis pipeline documentation — and actively seeking biology collaborators' review and input on these assumptions (rather than treating them as purely internal software implementation details) both improves assumption quality and builds collaborative trust.

4. **Develop shared vocabulary explicitly, not assuming disciplinary jargon will be understood:** Terms like "latency," "pipeline," "state machine," or "callback" have specific software engineering meanings that biology collaborators may not know; similarly, "plasticity," "LFP," "STDP," or "unit" have specific neuroscience meanings that may not map intuitively to software engineering experience. Investing in developing explicit shared vocabulary (and being willing to patiently explain software engineering concepts in biological terms, and to ask biology collaborators to explain biological concepts in ways accessible to a non-biologist) pays substantial dividends in avoiding misunderstandings that could produce software mismatched to biological reality.

### Q2: Describe how you would collaborate with hardware/electronics engineers on the signal acquisition hardware-software interface, and how you would contribute to (even if not solely design) hardware design decisions that have significant software implications.

**A:**
**Collaborative practices:**
1. **Engage hardware design discussions early regarding interface specification details that have major software implication:** Decisions made at the hardware level (ADC resolution and sampling rate, digital communication protocol between acquisition hardware and host computer, onboard filtering configuration, stimulation parameter range and resolution) have direct and often substantial implications for software architecture and performance — a software engineer who waits to engage with hardware design only after the hardware is finalized and discovers that the hardware interface requires software workarounds for features that would have been simple to include in hardware design at the outset has missed the most valuable window for cross-disciplinary input.

2. **Provide software's "requirements specification" to hardware early, framing software needs in hardware-actionable terms:** Software requirements that matter for hardware design (e.g., "I need sub-100µs deterministic latency from ADC sample completion to interrupt notification," "I need per-channel digital gain control accessible via software without hardware modification," "I need a hardware-enforced stimulation cutoff that cannot be overridden by software") should be explicitly communicated to hardware engineers in terms specific and actionable enough for hardware design consideration, rather than vague high-level "I need low latency" statements that leave hardware engineers unable to make appropriately-informed design trade-offs.

3. **Understand hardware constraints genuinely enough to make informed trade-off recommendations, not just a list of software wishlist features without understanding hardware cost:** A software engineer who understands that a specific feature would require adding an additional FPGA or redesigning the analog front-end amplifier chain understands the actual cost of requesting that feature and can make a genuinely informed trade-off recommendation (or negotiate a different software approach that achieves a similar outcome without requiring the costly hardware change) — this kind of hardware-cost-aware software engineering is much more valuable to a joint hardware-software development team than hardware-cost-agnostic software feature requests.

4. **Build joint hardware-software validation and testing procedures, not siloed hardware-only and software-only test plans:** Since hardware and software interact continuously, validation of correct system behavior (particularly for safety-critical functions, Topic 08) requires joint test procedures that exercise the complete hardware-software stack together — engaging hardware engineers as genuine partners in developing these joint test plans, rather than treating system-level validation as either purely a software concern or purely a hardware concern.

### Q3–Q13: (Representative additional topics)
- Collaborating with computational neuroscientists on decoding algorithm development (connecting to Topic 05)
- Working with ethics/regulatory affairs colleagues on compliance documentation (connecting to Topic 09)
- Managing expectations with research PIs and group leadership regarding realistic biocomputing system development timelines
- Facilitating productive disagreement when biological substrate behavior doesn't match software model assumptions
- Onboarding new team members with software-only backgrounds into biological substrate domain knowledge
- Cross-institutional collaboration considerations for large-scale biological computing research programs
- Knowledge management and documentation practices for preventing knowledge loss in fast-moving, cross-disciplinary teams
- Contributing software engineering perspective to research grant applications and experimental design planning
- Open-source collaboration and community-building within the nascent biological computing software tooling ecosystem
- Managing the specific communication challenges of presenting complex cross-disciplinary technical work to non-technical audiences

---

## Summary
Effective cross-functional collaboration requires the Biocomputer Software Engineer to invest genuinely in biological domain literacy as a core professional competency, engage hardware design discussions early with software-requirements translated into hardware-actionable terms, and build authentic bidirectional technical dialogue with biology and hardware colleagues — treating disciplinary boundary-crossing as a core, valued professional skill rather than an obstacle to the "real" software engineering work.
