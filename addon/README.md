What is FPGA(Field programmable gate array)

FPGA is hardware that is reconfigurable.

Imagine breadboard with lots of transistors and wires -- it is almost like that

You can remove or add any wire on breadboard ...

In FPGA you are actually doing the same thing with reprogramming.

Every time it starts it is fully empty and at start you need to reprogram it!

It can do that automatically from flash.

You can program it as many times you want!

Not sequential processing like on CPU.

FPGAs are ideal for parallel systems where multiple tasks must be performed simultaneously as they are electronically wired in the form of discrete programmable logic blocks which can be configured to suit the user’s needs.

What is HDL(Hardware description language)

It does not tell what to do like with CPU -- It is actually language that is describing hardware.

Verilog/VHDL can be used to describe electronic hardware at different levels of abstraction.

You can do it on logic gates level or on RTL level (like we will show later)...

Bistream is actually compiled binary, not representing CPU instructions, but defining actual hardware

Recommendation:

Verilog HDL by: Samir Palnitkar

Abstraction levels

https://www.doulos.com/knowhow/verilog_designers_guide/rtl_verilog/

Logic gates slides

https://slideplayer.com/slide/5313980/

Example: 

If you describe one micro controller in HDL and add more outputs for debugging so you can get internal registers status you will not slow down execution it will all run at the same speed as before.

If you put 5 independent CPUs inside FPGA not be slower. 

Speed will not depend on no of CPUs implemented.

They will all work independently.

Same is for modules -- you can add as many as you want (depending on FPGA size) -- you will not slow down other modules...

Be careful about clock domain crossing

If you have multiple clock sources be sure they are synchronized!

A clock domain crossing occurs whenever data is transferred from a flop driven by one clock to a flop driven by another clock. 

https://www.eetimes.com/document.asp?doc_id=1276114#
