# Lessons learned about AI coding during this build
**Architecting Milestone 1**
* We will allow future architecture to emerge from concrete requirements rather than implementing anticipated future architecture now.
* Design for change ≠ implement future changes now.
* What change does this protect us from? How speculative is that change? Can we leave ourselves room for that change without implementing the solution prematurely?
* Three tests for the right amount of separation/abstraction
  1. The Change Test: What foreseeable change does this boundary make easier? If you can't name one, don't add it yet.
  2. The Comprehension Test: Does separating this make the system easier for a human to understand, or does the reader now have to bounce among five files to understand one operation?
  3. The Responsibility Test: Are these genuinely different jobs? "Interact with the user" and "communicate with an external API" are meaningfully different responsibilities. That's a good separation.
* Architecture should manage complexity to make understanding easier for the reader and help focus their attention on the right things, not merely redistribute it across more files and folders.

