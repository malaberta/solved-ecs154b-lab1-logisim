Download Link: https://assignmentchef.com/product/solved-ecs154b-lab1-logisim
<br>
<h1></h1>

<ul>

 <li>Learn how to use Logisim.</li>

 <li>Lean how to use the circuit analyzer tool.</li>

 <li>Learn an alternative to combinational logic.</li>

</ul>

<h1>Logisim</h1>

<ul>

 <li>The project page for Logisim is at <a href="http://www.cburch.com/logisim">http://www.cburch.com/logisim</a><a href="http://www.cburch.com/logisim">.</a></li>

 <li>You can download Logisim on SourceForge for Windows and OS X at <a href="https://sourceforge.net/projects/circuit/">http://sourceforge.net/ </a><a href="https://sourceforge.net/projects/circuit/">projects/circuit/</a><a href="https://sourceforge.net/projects/circuit/">.</a> If you are using Linux, your package manager for your distribution may have Logisim as well.</li>

 <li>You can find a brief tutorial for Logisim on Professor Farrens’ class website at <a href="http://american.cs.ucdavis.edu/academic/ecs154a/postscript/logisim-tutorial.pdf">http://american.cs. </a><a href="http://american.cs.ucdavis.edu/academic/ecs154a/postscript/logisim-tutorial.pdf">edu/academic/ecs154a/postscript/logisim-tutorial.pdf</a><a href="http://american.cs.ucdavis.edu/academic/ecs154a/postscript/logisim-tutorial.pdf">.</a></li>

 <li>The <strong>User’s Guide </strong>and <strong>Library Reference </strong>in the Help menu in Logisim are also very helpful.</li>

</ul>

<h1>Introduction</h1>

When designing a circuit to implement a function, there are two different design routes that you can take: use pure combinational logic, or use a Read Only Memory (ROM). Combinational logic involves combining AND, OR, and NOT gates to implement the Boolean equation that you derive from the truth table. On the other hand, by using a ROM, you simply implement the truth table in hardware.

<h1>ROM Implementation</h1>

A memory unit can be viewed as simply a truth table in hardware. Here are the steps to creating a ROM implementation of a truth table.

<ol>

 <li>Create a ROM, where the number of addressing bits is equal to the number of inputs, and the databit width is equal to the number of output bits.</li>

 <li>Using the input bits as the address, fill in the entries of the ROM with the correct outputs for thatcombination of inputs.</li>

 <li>To get the output, address the ROM using the concatenation of the input signals.</li>

</ol>

<h2>Example</h2>

The following is an example of implementing the XOR function using microcode. On the next page is the truth table for XOR (⊕).

<table width="107">

 <tbody>

  <tr>

   <td width="26"> </td>

   <td colspan="2" width="81">XOR</td>

  </tr>

  <tr>

   <td width="26">X</td>

   <td width="26">Y</td>

   <td width="55">X ⊕ Y</td>

  </tr>

  <tr>

   <td width="26">0</td>

   <td width="26">0</td>

   <td width="55">0</td>

  </tr>

  <tr>

   <td width="26">0</td>

   <td width="26">1</td>

   <td width="55">1</td>

  </tr>

  <tr>

   <td width="26">1</td>

   <td width="26">0</td>

   <td width="55">1</td>

  </tr>

  <tr>

   <td width="26">1</td>

   <td width="26">1</td>

   <td width="55">0</td>

  </tr>

 </tbody>

</table>

Applying step 1, we first create a ROM with 2 address bits, because we have 2 inputs. Each entry is 1 bit wide, because there is only output. Next, we fill in the ROM using X and Y as the address bits.

<table width="162">

 <tbody>

  <tr>

   <td width="26">X</td>

   <td width="26">Y</td>

   <td width="62">Address</td>

   <td width="48">Value</td>

  </tr>

  <tr>

   <td width="26">0</td>

   <td width="26">0</td>

   <td width="62">0</td>

   <td width="48">0</td>

  </tr>

  <tr>

   <td width="26">0</td>

   <td width="26">1</td>

   <td width="62">1</td>

   <td width="48">1</td>

  </tr>

  <tr>

   <td width="26">1</td>

   <td width="26">0</td>

   <td width="62">2</td>

   <td width="48">1</td>

  </tr>

  <tr>

   <td width="26">1</td>

   <td width="26">1</td>

   <td width="62">3</td>

   <td width="48">0</td>

  </tr>

 </tbody>

</table>

The Logisim implementation is included with the given files for the assignment, in the subcircuit <strong>ROM XOR</strong>.

<h1>ROMs and Sequential Circuits</h1>

Here is how you can use a ROM to implement Moore sequential circuits. Instead of implementing the truth table, the ROM implements the next state transition table and the outputs in hardware. Here is how to do it:

<ol>

 <li>Create a ROM where the number of address bits is equal to (number of state bits) + (number of inputbits). The data bit width is equal to (number of state bits) + (number of output bits).</li>

 <li>Fill in the ROM using the state transition table. Each entry in the ROM contains the next state bitsalong with the output at that current state.</li>

 <li>To address the ROM, concatenate the next state bits from the ROM with the input signals. The nextstate portion of the output of the ROM will feed back into the input of the ROM.</li>

</ol>

<h2>Example</h2>

Suppose we want to create a sequential circuit that while it is in state 0, it outputs 01, when in state 1 it outputs 11, and changes between states whenever the input, X, is 1. The machine starts in state 0. The transition table for this machine would be as follows.

<table width="259">

 <tbody>

  <tr>

   <td colspan="3" width="201">State Transition Table</td>

   <td width="59"> </td>

  </tr>

  <tr>

   <td width="96">Current State</td>

   <td width="26">X</td>

   <td width="79">Next State</td>

   <td width="59">Output</td>

  </tr>

  <tr>

   <td width="96">0</td>

   <td width="26">0</td>

   <td width="79">0</td>

   <td width="59">01</td>

  </tr>

  <tr>

   <td width="96">0</td>

   <td width="26">1</td>

   <td width="79">1</td>

   <td width="59">01</td>

  </tr>

  <tr>

   <td width="96">1</td>

   <td width="26">0</td>

   <td width="79">1</td>

   <td width="59">11</td>

  </tr>

  <tr>

   <td width="96">1</td>

   <td width="26">1</td>

   <td width="79">0</td>

   <td width="59">11</td>

  </tr>

 </tbody>

</table>

By applying step 1, we would first create a ROM that has 2 address bits, 1 for the next state and 1 for the input X. For each address, the ROM has data entries that are 3 bits wide, 1 for the next state and 2 for the output. Applying step 2 and using the top bit in each entry in the ROM to store the next state and the bottom 2 for the output:

<table width="422">

 <tbody>

  <tr>

   <td width="96">Current State</td>

   <td width="26">X</td>

   <td width="62">Address</td>

   <td width="79">Next State</td>

   <td width="59">Output</td>

   <td width="100">Value in ROM</td>

  </tr>

  <tr>

   <td width="96">0</td>

   <td width="26">0</td>

   <td width="62">0</td>

   <td width="79">0</td>

   <td width="59">01</td>

   <td width="100">001(0x1)</td>

  </tr>

  <tr>

   <td width="96">0</td>

   <td width="26">1</td>

   <td width="62">1</td>

   <td width="79">1</td>

   <td width="59">01</td>

   <td width="100">101(0x5)</td>

  </tr>

  <tr>

   <td width="96">1</td>

   <td width="26">0</td>

   <td width="62">2</td>

   <td width="79">1</td>

   <td width="59">11</td>

   <td width="100">111(0x7)</td>

  </tr>

  <tr>

   <td width="96">1</td>

   <td width="26">1</td>

   <td width="62">3</td>

   <td width="79">0</td>

   <td width="59">11</td>

   <td width="100">011(0x3)</td>

  </tr>

 </tbody>

</table>

Because of the way that we decided to implement the machine, the top most output of the ROM feeds back into the top most bit of its input.

A Logisim implementation of this circuit is included with the assignment, in the subcircuit <strong>ROM Sequential</strong>. Note that the hex editor in Logisim expects hexadecimal values, so it is necessary to convert the concatenation of the bits from binary to hex, as shown.

<h2>Sequential Circuits using ROMs in Logisism</h2>

In order to implement sequential circuits with using ROM, the ROM must be synchronous. Logisim does not come with a built in synchronous ROM, but you can make your own by connecting a register to the output of the built-in ROM module.

<h1>Assignment</h1>

<ol>

 <li>Implement a combinational circuit using both combinational logic and a ROM.</li>

 <li>Implement a sequential circuit using only a ROM.</li>

</ol>

For each circuit, please create a sub-circuit with appropriately named inputs and outputs.

<h2>1.       Combinatorial Circuit</h2>

Implement the circuit that has the following truth table using both <strong>combinational logic </strong>and <strong>microcode</strong>.

<ul>

 <li>When creating the combinational circuit using combinational logic, you may only use splitters and these gates: AND, OR, NOT, XOR.</li>

</ul>

<strong>– </strong>In addition, the logic must be the minimal amount to express the truth table.

<ul>

 <li>When creating the combinational circuit using a ROM, you may only use the ROM module.</li>

 <li><strong>In </strong>are the inputs and <strong>Out </strong>are the outputs.</li>

 <li>All unspecified input and output combinations are don’t cares, as are the <strong>D</strong>s in the table.</li>

</ul>

<table width="417">

 <tbody>

  <tr>

   <td width="35">In7</td>

   <td width="35">In6</td>

   <td width="35">In5</td>

   <td width="35">In4</td>

   <td width="35">In3</td>

   <td width="35">In2</td>

   <td width="35">In1</td>

   <td width="36">In0</td>

   <td width="47">Out2</td>

   <td width="45">Out1</td>

   <td width="45">Out0</td>

  </tr>

  <tr>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="36">0</td>

   <td width="47">1</td>

   <td width="45">0</td>

   <td width="45">0</td>

  </tr>

  <tr>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="36">1</td>

   <td width="47">0</td>

   <td width="45">0</td>

   <td width="45">1</td>

  </tr>

  <tr>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">1</td>

   <td width="36">0</td>

   <td width="47">1</td>

   <td width="45">1</td>

   <td width="45">0</td>

  </tr>

  <tr>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">1</td>

   <td width="36">1</td>

   <td width="47">0</td>

   <td width="45">0</td>

   <td width="45">0</td>

  </tr>

  <tr>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">1</td>

   <td width="35">0</td>

   <td width="36">0</td>

   <td width="47">0</td>

   <td width="45">1</td>

   <td width="45">1</td>

  </tr>

  <tr>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">1</td>

   <td width="35">0</td>

   <td width="36">1</td>

   <td width="47">1</td>

   <td width="45">0</td>

   <td width="45">1</td>

  </tr>

  <tr>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">1</td>

   <td width="35">1</td>

   <td width="36">0</td>

   <td width="47">1</td>

   <td width="45">1</td>

   <td width="45">1</td>

  </tr>

  <tr>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">1</td>

   <td width="35">1</td>

   <td width="36">1</td>

   <td width="47">0</td>

   <td width="45">1</td>

   <td width="45">0</td>

  </tr>

  <tr>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">1</td>

   <td width="35">0</td>

   <td width="35">1</td>

   <td width="36">0</td>

   <td width="47">0</td>

   <td width="45">0</td>

   <td width="45">1</td>

  </tr>

  <tr>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">1</td>

   <td width="35">1</td>

   <td width="35">0</td>

   <td width="36">1</td>

   <td width="47">1</td>

   <td width="45">1</td>

   <td width="45">0</td>

  </tr>

  <tr>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">1</td>

   <td width="35">1</td>

   <td width="35">1</td>

   <td width="36">0</td>

   <td width="47">0</td>

   <td width="45">0</td>

   <td width="45">1</td>

  </tr>

  <tr>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">1</td>

   <td width="35">1</td>

   <td width="35">D</td>

   <td width="35">D</td>

   <td width="35">D</td>

   <td width="36">D</td>

   <td width="47">1</td>

   <td width="45">0</td>

   <td width="45">0</td>

  </tr>

  <tr>

   <td width="35">0</td>

   <td width="35">1</td>

   <td width="35">1</td>

   <td width="35">1</td>

   <td width="35">D</td>

   <td width="35">D</td>

   <td width="35">D</td>

   <td width="36">D</td>

   <td width="47">0</td>

   <td width="45">1</td>

   <td width="45">0</td>

  </tr>

  <tr>

   <td width="35">1</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">D</td>

   <td width="35">D</td>

   <td width="35">D</td>

   <td width="36">D</td>

   <td width="47">1</td>

   <td width="45">1</td>

   <td width="45">1</td>

  </tr>

  <tr>

   <td width="35">1</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">1</td>

   <td width="35">D</td>

   <td width="35">D</td>

   <td width="35">D</td>

   <td width="36">D</td>

   <td width="47">0</td>

   <td width="45">1</td>

   <td width="45">1</td>

  </tr>

  <tr>

   <td width="35">1</td>

   <td width="35">1</td>

   <td width="35">0</td>

   <td width="35">0</td>

   <td width="35">D</td>

   <td width="35">D</td>

   <td width="35">D</td>

   <td width="36">D</td>

   <td width="47">1</td>

   <td width="45">0</td>

   <td width="45">1</td>

  </tr>

  <tr>

   <td width="35">1</td>

   <td width="35">1</td>

   <td width="35">1</td>

   <td width="35">0</td>

   <td width="35">D</td>

   <td width="35">D</td>

   <td width="35">D</td>

   <td width="36">D</td>

   <td width="47">0</td>

   <td width="45">0</td>

   <td width="45">0</td>

  </tr>

  <tr>

   <td width="35">1</td>

   <td width="35">1</td>

   <td width="35">1</td>

   <td width="35">1</td>

   <td width="35">D</td>

   <td width="35">D</td>

   <td width="35">D</td>

   <td width="36">D</td>

   <td width="47">0</td>

   <td width="45">0</td>

   <td width="45">1</td>

  </tr>

 </tbody>

</table>

Your sub-circuit should have the following inputs and outputs:

<strong>Inputs</strong>

<ul>

 <li>In7-0</li>

</ul>

<strong>Outputs</strong>

<ul>

 <li>Out: The concatenation of Out2-0, with Out2 as the top most bit and Out0 as the bottom most bit.</li>

</ul>

<h3>The Circuit Analyzer Tool</h3>

Don’t be intimidated by the number of inputs when doing the combinational circuit. You can use Logisim’s <strong>Analyze Circuit </strong>tool, in the Project drop-down menu, to have Logisim build the circuit for you. To learn how to use it, click on Help → User’s Guide. In the User Guide, click on Combinational Analysis and read how to use it. You will find this tool very helpful in this and future labs.

<h2>2.      Sequential Circuit</h2>

For this section, you may only use the ROM, Register, Splitter, and Clock modules in Logisim. Refrain from using any logic gates in this part. The sequential circuit example <strong>ROM Sequential </strong>discussed above discusses in detail how you should solve this part.

Implement a Moore Model sequential circuit that takes as input a stream of bits. <strong>There are two separate conditions to keep track of:</strong>

If at least 2 bits out of every 4 are 1, the circuit should output 1 after seeing the 4th bit. <strong>Additionally</strong>, if the circuit detects that the 4 bit sequence was 0000, then it will also output 1 after seeing the 4th bit.

Otherwise, the circuit outputs 0 at all other times.

Here is an example input and output, with bits being input to the machine from <strong>left to right</strong>:

Input:            0001 0000 0011 1111 0100

Output: 0000 0000 1000 1000 1000 0

Remember, since we are implementing a Moore model, the output will be delayed by one clock tick. Your sub-circuit should have the following inputs and outputs:

<h3>Inputs</h3>

<ul>

 <li>Clock: The system clock.</li>

 <li>X: The current value in the input bit stream.</li>

</ul>

<strong>Outputs</strong>

<ul>

 <li>Out: The output from your sequential circuit.</li>

</ul>

<h1>Testing</h1>

You will be provided with the following circuits to facilitate testing.

<ul>

 <li><strong>Combinational Input</strong>: Generates the inputs for the combinational circuit.

  <ul>

   <li>Inputs:</li>

  </ul></li>

</ul>

∗ Clock: The system clock.

<ul>

 <li>Outputs: From top to bottom, In7-In0, the input signals to the combinational circuit.</li>

</ul>

<ul>

 <li><strong>Sequential Input</strong>: Generates the inputs for the sequential circuit.

  <ul>

   <li>Inputs:</li>

  </ul></li>

</ul>

∗ Clock: The system clock.

<ul>

 <li>Outputs:</li>

</ul>

∗ X: The input bit stream for your sequential circuit.

∗ NotDone: 1 when the test is still ongoing. Connect this to the <em>sel </em>input on your ROM.

You will also be provided with the following log files to test if your circuits are correct:

<h2>• CombOut.correct.log</h2>

<ul>

 <li>The log file containing the correct outputs for the combinational logic circuit using combinational logic.</li>

 <li>The X’s in the file indicate don’t cares.</li>

</ul>

<h2>• ROMCombOut.correct.log</h2>

<ul>

 <li>The log file containing the correct outputs for the combinational logic circuit using a ROM.</li>

 <li>The X’s in the file indicate don’t cares.</li>

</ul>

<h2>• ROMSeqOut.correct.log</h2>

<ul>

 <li>The log file containing the correct outputs for the sequential circuit using a ROM.</li>

 <li>The X’s in the file indicate don’t cares.</li>

</ul>

We will be testing your code using Logisim’s logging feature. To log the results of your program, do the following:

<ol>

 <li>Attach a probe or pin to the wires that you want to log, and give it a name.</li>

 <li>Click Simulate → Logging.</li>

 <li>In the Selection tab, select the signals you want to log.</li>

 <li>Click on the File tab.</li>

 <li>Select a file to log the signals to.</li>

</ol>

You will need to create three separate log files, one for each sub-circuit:

<table width="509">

 <tbody>

  <tr>

   <td width="26"> </td>

   <td colspan="3" width="89"> </td>

   <td colspan="2" width="50"> </td>

   <td colspan="4" width="369">CombOut.log</td>

   <td width="26"> </td>

  </tr>

  <tr>

   <td width="26"> </td>

   <td colspan="3" width="89">Signal Name</td>

   <td colspan="2" width="50">Radix</td>

   <td colspan="4" width="369">Description</td>

   <td width="26"> </td>

  </tr>

  <tr>

   <td width="26"> </td>

   <td colspan="3" width="89">Input</td>

   <td colspan="2" width="50">2</td>

   <td colspan="4" width="369">The concatenation of In7-0.</td>

   <td width="26"> </td>

  </tr>

  <tr>

   <td width="26"> </td>

   <td colspan="3" width="89">CombOut</td>

   <td colspan="2" width="50">2</td>

   <td colspan="4" width="369">The concatenation of Out2-0 from the combinational circuit.</td>

   <td width="26"> </td>

  </tr>

  <tr>

   <td colspan="3" width="105"> </td>

   <td colspan="2" width="50"> </td>

   <td colspan="6" width="405">ROMCombOut.log</td>

  </tr>

  <tr>

   <td colspan="3" width="105">Signal Name</td>

   <td colspan="2" width="50">Radix</td>

   <td colspan="6" width="405">Description</td>

  </tr>

  <tr>

   <td colspan="3" width="105">Input</td>

   <td colspan="2" width="50">2</td>

   <td colspan="6" width="405">The concatenation of In7-0.</td>

  </tr>

  <tr>

   <td colspan="3" width="105">ROMCombOut</td>

   <td colspan="2" width="50">2</td>

   <td colspan="6" width="405">The concatenation of Out2-0 from the ROM combinational circuit.</td>

  </tr>

  <tr>

   <td colspan="2" width="88"> </td>

   <td colspan="5" width="91"> </td>

   <td width="50"> </td>

   <td width="244">ROMSeqOut.log</td>

   <td colspan="2" width="88"> </td>

  </tr>

  <tr>

   <td colspan="2" width="88"> </td>

   <td colspan="5" width="91">Signal Name</td>

   <td width="50">Radix</td>

   <td width="244">Description</td>

   <td colspan="2" width="88"> </td>

  </tr>

  <tr>

   <td colspan="2" width="88"> </td>

   <td colspan="5" width="91">X</td>

   <td width="50">2</td>

   <td width="244">The input bit stream X.</td>

   <td colspan="2" width="88"> </td>

  </tr>

  <tr>

   <td colspan="2" width="88"> </td>

   <td colspan="5" width="91">ROMSeqOut</td>

   <td width="50">2</td>

   <td width="244">The output from the sequential circuit.</td>

   <td colspan="2" width="88"> </td>

  </tr>

  <tr>

   <td width="24"></td>

   <td width="62"></td>

   <td width="17"></td>

   <td width="10"></td>

   <td width="40"></td>

   <td width="10"></td>

   <td width="12"></td>

   <td width="50"></td>

   <td width="214"></td>

   <td width="48"></td>

   <td width="20"></td>

  </tr>

 </tbody>

</table>

To see if your circuit is correct, use the Python program, tester.py, included with assignment. To use it, type, in your command line, with all files in the same directory:

python tester.py correct log file your log file

where correct log file is the file that contains the correct signals, and your log file is the name of the log file you have your signals in. For example, to test if your combinational circuit is correct, you would type:

python tester.py CombOut.correct.log CombOut.log

if your log file was named CombOut.log.

If you are using Windows, you may want to add Python to your system path to make testing easier, if you have not already.

Note: the Logisim logger is a ”lazy” logger, in that it only logs a value if there is a change in the output value. This causes the log file’s output to be different from what one would expect for a given output. Hence, you will need to test all the problems manually and finally validate by using tester.py as stated above to match your output to the correct output.

<h2>Resetting the Log Files</h2>

If your circuit has some errors the first time, in order to retest your file, you must do the following steps in this order:

<ol>

 <li>Delete the contents of your log file except for the headers, the names of the signals.</li>

 <li>Reset your circuit by pressing Ctrl + R, or by going to Simulate → Reset Simulation.</li>

 <li>Simulate again.</li>

 <li>Run py again.</li>

</ol>