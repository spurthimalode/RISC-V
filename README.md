# RISC-V
## TABLE OF CONTENTS
## Day 3
**Digital Logic with TL-Verilog and Makerchip**  
+ [Combinational Logic in TL-Verilog using Makerchip](#combinational-logic-in-tl-verilog-using-makerchip)
+ [Sequential Logic](#sequential-logic)
+ [Pipelined Logic](#pipelined-logic)
+ [Validity](#validity)

## Combinational Logic in TL-Verilog using Makerchip
<details>
<summary> Introduction </summary>

+ **Logic Gates**
  Logic gates are fundamental electronic devices or building blocks used in digital circuits to perform basic logical operations on binary inputs (0 and 1) and produce binary outputs. Each type of logic gate follows specific rules and logic expressions to determine its output based on the input signals.
  
  ![image](https://github.com/spurthimalode/RISC-V/assets/142222859/64e6f0f7-5e72-40a9-8137-ad7ab2cb98cd)

  + **Boolean Operation**

  Boolean operations are fundamental operations in Boolean algebra, a mathematical structure dealing with variables that can take on one of two values, typically denoted as true (1) and false (0).

  ![image](https://github.com/spurthimalode/RISC-V/assets/142222859/c7c98c07-4237-4cdc-a465-6068d646fcbd)

  + **Multiplexer**
 
   A 2:1 multiplexer (also known as a 2-to-1 mux) is a digital circuit that selects one of two input data lines and directs it to a single output line based on a control signal. The control signal determines which of the two input lines is transmitted to the output.
  
    ![image](https://github.com/spurthimalode/RISC-V/assets/142222859/6d10e1dd-b9d7-43d1-8385-1f31afa2f4b9)

+ **Chaining Ternary Operator**
  
    ![image](https://github.com/spurthimalode/RISC-V/assets/142222859/ee1e9077-de5b-44c5-b3fb-a0061cb039ad)
</details>
<details>
<summary>Labs</summary>

## Makerchip platform
+ Go to http://makerchip.com/
+ Click `IDE`
+ Open `Tutorials` then `Validity Tutorial`
+ Click `Load Pythogorean Example`
+ Split planes and move tabs.
+ Zoom/pan in Diagram with mouse wheel and drag.
+ Zoom waveform with `Zoom In` button.
+ Click `$bb_sq` in waveform to highlight in the diagram.

![image](https://github.com/spurthimalode/RISC-V/assets/142222859/994037ef-8a3c-4dae-a12e-8f16d84fbaf4)

## A)Inverter
+ Open `Examples`(under `Tutorials`).
+ Load `Makerchip Default Template`.
+ Make an inverter.
+ On line 16, in place of `//..` , type `$out = ! $in1;` (preserve 3-space indentation, no tabs).
+ Compile (`E` menu).

  ![image](https://github.com/spurthimalode/RISC-V/assets/142222859/60a27f72-bc0b-4b77-9384-bce8a08f2ec0)
  
## B) OR Gate
+  On line 16, in place of `//..` , type
  ```v
  $out = $in1 | $in2;
  ```
![image](https://github.com/spurthimalode/RISC-V/assets/142222859/1da09201-3344-4a33-a080-c22ec353b765)

## C) Vectors
+  On line 16, in place of `//..` , type

 ```v
  $out[4:0] = $in1[3:0] + $in2[3:0];
```
![image](https://github.com/spurthimalode/RISC-V/assets/142222859/e98da986-5a16-495b-ad3e-9f2212d15b9b)

## D) MUX
![image](https://github.com/spurthimalode/RISC-V/assets/142222859/5d9c152f-1c38-4f3f-b4c3-ae0343075876)

+ ```v
  $out = $sel ? $in1 : $in2;
  ```

![image](https://github.com/spurthimalode/RISC-V/assets/142222859/519d64de-67f2-4a69-8d7c-2b8444079eff)
+ Modified the mux to operate on vectors.
  ![image](https://github.com/spurthimalode/RISC-V/assets/142222859/f0a36fbd-4bf9-4cae-9632-81b1f6295866)

  ```v
     $out[7:0] = $sel ? $in1[7:0] : $in2[7:0];
  ```
![image](https://github.com/spurthimalode/RISC-V/assets/142222859/f3fbc6f4-8cc3-4e16-964e-ecb0a2e11daf)

## E) Simple Calculator
![image](https://github.com/spurthimalode/RISC-V/assets/142222859/c3bd6bc8-250b-4822-b568-2a6ae85dd008)

```v
$reset = *reset;
$val1[31:0] = $rand1[3:0];
$val2[31:0] = $rand2[3:0];
$sum[31:0] = $val1[31:0] + $val2[31:0];
$diff[31:0] = $val1[31:0] - $val2[31:0];
$prod[31:0] = $val1[31:0] * $val2[31:0];
$quot[31:0] = $val1[31:0] / $val2[31:0];
$out[31:0] = $op[1] ? ($op[0] ? $quot : $prod)
                    : ($op[0] ? $diff : $sum);
```

![image](https://github.com/spurthimalode/RISC-V/assets/142222859/d40ac0b0-773b-4a02-b81e-f19b4d90fb6f)

</details>

## Sequential Logic
<details>
  <summary>Introduction</summary>
  
  ![image](https://github.com/spurthimalode/RISC-V/assets/142222859/d7aa7e1f-422d-41d7-8f0e-5147f96fbfba)

  ![image](https://github.com/spurthimalode/RISC-V/assets/142222859/ea27249a-824a-44cf-935a-390b827a00a1)

</details>
<details>
  <summary>Labs </summary>
  
  ## A) Fibonacci Series reset
  ![image](https://github.com/spurthimalode/RISC-V/assets/142222859/d1ccb834-e697-4200-9db0-473487cbf32c)

  ```
$fib[31:0] = $reset ? 1 : (>>1$fib + >>2$fib);
  ```
![image](https://github.com/spurthimalode/RISC-V/assets/142222859/a9e49540-f3cb-441a-9d54-5e0ac746f1d2)

## B) Counter
```
   $cnt[31:0] = $reset ? 0 : (1 + >>1$cnt);
```
![image](https://github.com/spurthimalode/RISC-V/assets/142222859/7b4223fd-5cf6-4a4c-8e2a-a9729867eac2)

## C) Sequential calculator
```
 $reset = *reset;
 $val2[31:0] = $rand2[3:0]; 
 $val1[31:0] = >>1$out[31:0];
 $sum[31:0] = $val1[31:0] + $val2[31:0];
 $diff[31:0] = $val1[31:0] - $val2[31:0];
 $prod[31:0] = $val1[31:0] * $val2[31:0];
 $quot[31:0] = $val1[31:0] / $val2[31:0];
 $out[31:0] = $reset ? 32'b0 :
              ($op[1] ? ($op[0] ? $quot : $prod)
                      : ($op[0]? $diff : $sum));
```
![image](https://github.com/spurthimalode/RISC-V/assets/142222859/539fd6df-3acb-4010-ab6d-cd2d4ab6ce3d)

</details>

## Pipelined Logic
<details>
  <summary>Introduction</summary>

  
</details>

<details>
  <summary>Labs</summary>

  
</details>

## Validity
<details>
  <summary>Introduction</summary>

  
</details>

<details>
  <summary>Labs</summary>

  
</details>

## Day 4
**Basic RISC-V CPU Microarchitecture**
+ [Introduction](#introduction)
+ [Fetch and Decode](#fetch-and-decode)
+ [RISCV Control Logic](#riscv-control-logic)


## Day 5
**Complete Pipelined RISC-V CPU Micro-architecture**
+ [Pipelining the CPU](#pipelining-the-cpu)
+ [Solutions to Pipeline Hazards](#solutions-to-pipeline-hazards)
+ [Load/Store Instructions and Completing RISC-V CPU](#load/store-instructions-and-completing-risc-v-cpu)
