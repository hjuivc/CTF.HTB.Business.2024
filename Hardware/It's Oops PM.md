# It's Oops PM

With the location of the underground bunker secured, the crew embarks on the next phase of their plan: assessing the feasibility of creating an underground tunnel to bypass the super mutant camp. They secure samples of water, soil, and air near the area. Scouring the wasteland for salvageable equipment, they stumble upon a dilapidated research facility where they find a cache of environmental sensors. Examining these sensors, the crew discovers they communicate with a satellite and contain a crypto-processor that encrypts their transmissions. After hand-drawing the diagrams and emulating the silicon chip's logic with VHDL, they uncover what appears to be a backdoor in the embedded logic that only triggers when a specific input is given to the system. Determined to exploit this, they turn to their tech specialist. Can you connect to the satellite and activate it?

```sh
┌──(kali㉿kali)-[~/Desktop/hardware_its_oops_pm]
└─$ nc 94.237.63.135 36642           

The input must be a binary signal of 16 bits.

Input : 1111111111101001
Output: 0110001111100001

You triggered the backdoor here is the flag: HTB{4_7yp1c41_53cu23_TPM_ch1p}
```