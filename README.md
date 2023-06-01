# **VSD OpenLANE Physical Design Workshop using SKY130 PDK**
## Day 1 : Inception of open-source EDA, OpenLANE and SKY130 PDK
### Introduction to RISC-V
RISC-V is an open-source instruction set architecture (ISA) that is adopted in the world of computer architecture and processor design. It was originally developed at the University of California, Berkeley in 2010 and has since grown into a global collaboration of researchers and industry experts. The key characteristic of RISC-V is its simplicity and modularity. It follows the Reduced Instruction Set Computer (RISC) design philosophy, which emphasizes a small and streamlined set of instructions that are easy to decode and execute. RISC-V offers a base set of instructions, called the "RV32I," which provides essential operations for general-purpose computing. Additional optional instruction sets, such as RV32F for single-precision floating-point operations or RV64G for 64-bit computing, can be added to meet specific application requirements. One of the major advantages of RISC-V is its open nature. The ISA specifications, reference implementations, and software tools are freely available, allowing anyone to study, modify, or implement their own RISC-V processors without licensing fees or restrictions. This openness has fostered a vibrant ecosystem of hardware designers, software developers, and researchers who collaborate and innovate around the RISC-V architecture.

### How the software applications run on the hardware ?
All the software applications we use in our daily lives rely on hardware to run. The system software is responsible for translating the application program into binary language, which the hardware can understand and execute. The primary components of system software include the Operating System (OS), Compiler, and Assembler. The OS plays a crucial role in managing various aspects of the computer system. It provides an environment for the application program to run and handles tasks such as memory management, process scheduling, and input/output operations. Depending on the underlying architecture, such as MIPS, x86, x64, or RISC-V, the OS translates the application program into assembly language instructions. The compiler is responsible for converting high-level programming languages, like C or Java, into assembly-level language instructions. This translation process is influenced by the specific architecture on which the software will be executed. Different architectures have their own instruction sets, and the compiler ensures that the instructions generated are compatible with the targeted architecture. Once the code is in assembly language, the assembler comes into play. It takes the assembly code and translates it into binary code, which is a sequence of 0s and 1s that can be directly dumped into the hardware.

### Open-Source Digital ASIC Design
![Opensoure ASIC req](https://github.com/KanishR1/vsd_openlane_workshop/assets/88330171/7c3b4a4d-ff10-4b12-89db-0e6c8cb6a612)
Designing Application Specific Integraded Circuits (ASICs) basically requires three elements : RTL IPs, EDA Tools and PDKs.

**RTL IPs**, or Register Transfer Level Intellectual Property, refer to pre-designed and pre-verified digital hardware components or blocks that are described at the Register Transfer Level (RTL). RTL is a hardware description language (HDL) representation of a digital circuit or a portion of a circuit. In the context of integrated circuit (IC) design, an IP refers to a reusable building block that can be integrated into a larger design. RTL IPs, specifically, are designed at the register transfer level, which represents the flow of data between registers and the operations performed on that data.These IPs can be licensed from IP vendors or developed in-house. They provide a level of abstraction that allows designers to focus on higher-level design aspects rather than implementing low-level details from scratch. RTL IPs offer various advantages, such as improved productivity, faster time-to-market, and increased design reliability. By using RTL IPs, designers can leverage optimized and well-tested building blocks, reducing the likelihood of errors and bugs. Additionally, using RTL IPs promotes design reuse, enabling designers to create complex systems by assembling and integrating different IP blocks.

**EDA (Electronic Design Automation) tools** are software applications used in the design, development, and analysis of electronic systems, including integrated circuits (ICs), printed circuit boards (PCBs), and other electronic components. These tools automate various tasks involved in the design process, increasing efficiency and reducing time-to-market.

**Process Design Kit (PDK)** is a set of files used within the semiconductor industry to model a fabrication process for the design tools used to design an integrated circuit.  PDK’s are often specific to a foundry, and may be subject to a non-disclosure agreement.  While most PDK’s are proprietary to a foundry, certain PDKs are opensource and entirely within the public domain.Traditionally, PDKs have been proprietary and provided by semiconductor foundries, limiting access and customization options for IC designers. However, open-source PDKs aim to promote collaboration, innovation, and accessibility by making the design kit freely available to the community. By providing an open-source PDK, designers can modify and customize the kit to suit their specific requirements. This flexibility allows for greater innovation, collaboration, and knowledge sharing within the design community. It also lowers the barriers to entry for new designers and encourages participation in the development of new ICs and electronic systems. Some of the  open-source PDKs are : SKY130, GFU180, ASAP7 etc

### Simplified RTL to GDSII flow 
![rtl2gds2](https://github.com/KanishR1/vsd_openlane_workshop/assets/88330171/9ebd56da-1b8f-4f62-8ab0-9a0db0a0a1fc)
The RTL to GDSII flow basically involves :
1. **RTL Design** -  The process begins with the RTL design phase, where the digital circuit is described using a hardware description language (HDL) like VHDL or Verilog. The RTL description captures the functional behavior of the circuit, specifying its logic and data paths.

2. **RTL Synthesis** - RTL synthesis converts the high-level RTL description into a gate-level netlist. This stage involves mapping the RTL code to a library of standard cells (pre-designed logic elements) and optimizing the resulting gate-level representation for area, power, and timing. The output of RTL synthesis is typically in a format called the gate-level netlist.

3. **Floor and Power Planning** - is a crucial step in the digital design flow that involves partitioning the chip's area and determining the placement of major components and functional blocks. It establishes an initial high-level layout and defines the overall chip dimensions, locations of critical modules, power grid distribution, and I/O placement.The primary goals of floor planning are: Area Partitioning, Power Distribution, Signal Flow and Interconnect Planning, Placement of Key Components, Design Constraints and Optimization.

4. **Placement** - Placement involves assigning the physical coordinates to each gate-level cell on the chip's layout. The placement process aims to minimize wirelength, optimize signal delay, and satisfy design rules and constraints. Modern placement algorithms use techniques like global placement and detailed placement to achieve an optimal placement solution.

5. **Clock Tree Synthesis** - Clock tree synthesis (CTS) is a crucial step in the digital design flow that involves constructing an optimized clock distribution network within an integrated circuit (IC). The primary goal of CTS is to ensure balanced and efficient clock signal distribution to all sequential elements (flip-flops, registers) within the design, minimizing clock skew and achieving timing closure.

6. **Routing** - Routing connects the gates and interconnects on the chip based on the placement information. It involves determining the optimal paths for the wires and vias that carry signals between different components. The routing process needs to adhere to design rules, avoid congestion, and optimize for factors like signal integrity, power, and manufacturability.

7. **Sign-off** - Sign-off analysis refers to the final stage of the electronic design process, where comprehensive verification and analysis are performed to ensure that the design meets all the necessary requirements and specifications. It involves a series of checks and simulations to confirm that the design is ready for fabrication and meets the desired functionality, performance, power, and reliability targets. 

8. **GDSII File Generation** - Once the layout is verified and passes all checks, the final step is to generate the GDSII file format, which represents the complete physical layout of the chip. The GDSII file contains the geometric information necessary for fabrication, including the shapes, layers, masks, and other relevant details.

### Introduction to OpenLANE
OpenLane is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, Magic, Netgen, CVC, SPEF-Extractor, KLayout and a number of custom scripts for design exploration and optimization. It also provides a number of custom scripts for design exploration and optimization. The flow performs all ASIC implementation steps from RTL all the way down to GDSII. Currently, it supports both A and B variants of the sky130 PDK, the C variant of the gf180mcu PDK, and instructions to add support for other (including proprietary) PDKs are documented. OpenLane abstracts the underlying open source utilities, and allows users to configure all their behavior with just a single configuration file.

OpenLane integrated several key open source tools over the execution stages:
1. RTL Synthesis, Technology Mapping, and Formal Verification : yosys + abc
2. Static Timing Analysis: OpenSTA
3. Floor Planning: init_fp, ioPlacer, pdn and tapcell
4. Placement: RePLace (Global), Resizer and OpenPhySyn (formerly), and OpenDP (Detailed)
5. Clock Tree Synthesis: TritonCTS
6. Fill Insertion: OpenDP/filler_placement
7. Routing: FastRoute or CU-GR (formerly) and TritonRoute (Detailed) or DR-CU
8. SPEF Extraction: OpenRCX or SPEF-Extractor (formerly)
9. GDSII Streaming out: Magic and KLayout
10. DRC Checks: Magic and KLayout
11. LVS check: Netgen
12. Antenna Checks: Magic
13. Circuit Validity Checker: CVC

### OpenLANE ASIC Design flow
![flow_v1](https://github.com/KanishR1/vsd_openlane_workshop/assets/88330171/87ecc681-ab20-4c14-adae-a72c5cacfc70)

### OpenLANE Direcctory Structure
```
.
|-- AUTHORS.md
|-- CONTRIBUTING.md
|-- LICENSE
|-- Makefile
|-- README.md
|-- clean_runs.tcl
|-- conf.py
|-- configuration
|   |-- README.md
|   |-- checkers.tcl
|   |-- cts.tcl
|   |-- floorplan.tcl
|   |-- general.tcl
|   |-- lvs.tcl
|   |-- placement.tcl
|   |-- routing.tcl
|   `-- synthesis.tcl
|-- default.cvcrc
|-- designs
|   |-- 151
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- ALU.v
|   |       |-- ALUdec.v
|   |       |-- ALUop.vh
|   |       |-- Cache.v
|   |       |-- DataSRAMs.v
|   |       |-- ExecuteStage.v
|   |       |-- FetchDecodeStage.v
|   |       |-- Memory141.v
|   |       |-- Opcode.vh
|   |       |-- RegisterFile.v
|   |       |-- Riscv141.v
|   |       |-- TagSRAMs.v
|   |       |-- WriteBackStage.v
|   |       |-- backup_mem.v
|   |       |-- const.vh
|   |       |-- controller.v
|   |       |-- datapath.v
|   |       |-- no_cache_mem.v
|   |       |-- riscv_arbiter.v
|   |       `-- riscv_top.v
|   |-- APU
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       `-- APU.v
|   |-- BM64
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- BM64.sdc
|   |       `-- BM64.v
|   |-- PPU
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       `-- PPU.v
|   |-- README.md
|   |-- aes
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- aes.sdc
|   |       |-- aes.v
|   |       `-- aes_core.sdc
|   |-- aes128
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- aes128.sdc
|   |       `-- aes128.v
|   |-- aes192
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- aes192.sdc
|   |       `-- aes192.v
|   |-- aes256
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- aes256.sdc
|   |       `-- aes256.v
|   |-- aes_cipher
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- aes.v.x
|   |       |-- aes_cipher.v
|   |       |-- aes_key_expand_128.v
|   |       |-- aes_rcon.v
|   |       |-- aes_sbox.v
|   |       `-- timescale.v
|   |-- aes_core
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- aes.sdc
|   |       |-- aes.v
|   |       |-- aes_core.sdc
|   |       `-- aes_core.v
|   |-- blabla
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- blabla.sdc
|   |       `-- blabla.v
|   |-- chacha
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- chacha.sdc
|   |       `-- chacha.v
|   |-- cic_decimator
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       `-- cic_decimator.v
|   |-- des
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- 3des.v
|   |       `-- des.sdc
|   |-- des3
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- 3des.v
|   |       `-- des3.sdc
|   |-- digital_pll_sky130_fd_sc_hd
|   |   |-- config.tcl
|   |   `-- src
|   |       |-- digital_pll.v
|   |       |-- digital_pll_controller.v
|   |       `-- ring_osc2x13.v
|   |-- genericfir
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- genericfir.sdc
|   |       `-- genericfir.v
|   |-- inverter
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       `-- inverter.v
|   |-- jpeg_encoder
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- dct.v
|   |       |-- dct_cos_table.v
|   |       |-- dct_mac.v
|   |       |-- dctu.v
|   |       |-- dctub.v
|   |       |-- div_su.v
|   |       |-- div_uu.v
|   |       |-- fdct.v
|   |       |-- jpeg.v
|   |       |-- jpeg_encoder.v
|   |       |-- jpeg_qnr.v
|   |       |-- jpeg_rle.v
|   |       |-- jpeg_rle1.v
|   |       |-- jpeg_rzs.v
|   |       `-- zigzag.v
|   |-- ldpc_decoder_802_3an
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       `-- ldpc_decoder_802_3an.v
|   |-- ldpcenc
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       `-- ldpcenc.v
|   |-- manual_macro_placement_test
|   |   |-- config.tcl
|   |   |-- macro_placement.cfg
|   |   |-- macros
|   |   |   |-- gds
|   |   |   |   `-- spm.gds
|   |   |   `-- lef
|   |   |       `-- spm.lef
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       `-- design.v
|   |-- md5
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- md5.sdc
|   |       `-- md5.v
|   |-- ocs_blitter
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       `-- ocs_blitter.v
|   |-- picorv32a
|   |   |-- config.tcl
|   |   |-- runs
|   |   |   |-- 31-05_14-08
|   |   |   |   |-- OPENLANE_VERSION
|   |   |   |   |-- PDK_SOURCES
|   |   |   |   |-- cmds.log
|   |   |   |   |-- config.tcl
|   |   |   |   |-- logs
|   |   |   |   |   |-- 0-prep_runtime.txt
|   |   |   |   |   |-- cts
|   |   |   |   |   |-- cvc
|   |   |   |   |   |-- floorplan
|   |   |   |   |   |-- flow_summary.log
|   |   |   |   |   |-- klayout
|   |   |   |   |   |-- lvs
|   |   |   |   |   |-- magic
|   |   |   |   |   |-- placement
|   |   |   |   |   |-- routing
|   |   |   |   |   `-- synthesis
|   |   |   |   |       |-- 1-yosys.log
|   |   |   |   |       |-- 1-yosys_runtime.txt
|   |   |   |   |       |-- 2-opensta
|   |   |   |   |       `-- 2-opensta_runtime.txt
|   |   |   |   |-- reports
|   |   |   |   |   |-- cts
|   |   |   |   |   |-- cvc
|   |   |   |   |   |-- floorplan
|   |   |   |   |   |-- klayout
|   |   |   |   |   |-- lvs
|   |   |   |   |   |-- magic
|   |   |   |   |   |-- placement
|   |   |   |   |   |-- routing
|   |   |   |   |   `-- synthesis
|   |   |   |   |       |-- 1-yosys_4.chk.rpt
|   |   |   |   |       |-- 1-yosys_4.stat.rpt
|   |   |   |   |       |-- 1-yosys_dff.stat
|   |   |   |   |       |-- 1-yosys_pre.stat
|   |   |   |   |       |-- 2-opensta.min_max.rpt
|   |   |   |   |       |-- 2-opensta.rpt
|   |   |   |   |       |-- 2-opensta.slew.rpt
|   |   |   |   |       |-- 2-opensta.timing.rpt
|   |   |   |   |       |-- 2-opensta_tns.rpt
|   |   |   |   |       `-- 2-opensta_wns.rpt
|   |   |   |   |-- results
|   |   |   |   |   |-- cts
|   |   |   |   |   |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |   |   |-- cvc
|   |   |   |   |   |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |   |   |-- floorplan
|   |   |   |   |   |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |   |   |-- klayout
|   |   |   |   |   |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |   |   |-- lvs
|   |   |   |   |   |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |   |   |-- magic
|   |   |   |   |   |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |   |   |-- placement
|   |   |   |   |   |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |   |   |-- routing
|   |   |   |   |   |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |   |   `-- synthesis
|   |   |   |   |       |-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |   |       `-- picorv32a.synthesis.v
|   |   |   |   `-- tmp
|   |   |   |       |-- cts
|   |   |   |       |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |       |-- cvc
|   |   |   |       |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |       |-- floorplan
|   |   |   |       |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |       |-- klayout
|   |   |   |       |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |       |-- lvs
|   |   |   |       |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |       |-- magic
|   |   |   |       |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |       |-- merged.lef
|   |   |   |       |-- merged_unpadded.lef
|   |   |   |       |-- met_layers_list.txt
|   |   |   |       |-- placement
|   |   |   |       |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |       |-- routing
|   |   |   |       |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |       |-- sky130_fd_sc_hd__tt_025C_1v80.no_pg.lib
|   |   |   |       |-- synthesis
|   |   |   |       |   |-- hierarchy.dot
|   |   |   |       |   |-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |       |   `-- yosys.sdc
|   |   |   |       |-- tracks_copy.info
|   |   |   |       |-- trimmed.lib
|   |   |   |       `-- trimmed.lib.exclude.list
|   |   |   `-- 31-05_14-17
|   |   |       |-- OPENLANE_VERSION
|   |   |       |-- PDK_SOURCES
|   |   |       |-- cmds.log
|   |   |       |-- config.tcl
|   |   |       |-- logs
|   |   |       |   |-- 0-prep_runtime.txt
|   |   |       |   |-- cts
|   |   |       |   |-- cvc
|   |   |       |   |-- floorplan
|   |   |       |   |-- flow_summary.log
|   |   |       |   |-- klayout
|   |   |       |   |-- lvs
|   |   |       |   |-- magic
|   |   |       |   |-- placement
|   |   |       |   |-- routing
|   |   |       |   `-- synthesis
|   |   |       |       |-- 1-yosys.log
|   |   |       |       |-- 1-yosys_runtime.txt
|   |   |       |       |-- 2-opensta
|   |   |       |       `-- 2-opensta_runtime.txt
|   |   |       |-- reports
|   |   |       |   |-- cts
|   |   |       |   |-- cvc
|   |   |       |   |-- floorplan
|   |   |       |   |-- klayout
|   |   |       |   |-- lvs
|   |   |       |   |-- magic
|   |   |       |   |-- placement
|   |   |       |   |-- routing
|   |   |       |   `-- synthesis
|   |   |       |       |-- 1-yosys_4.chk.rpt
|   |   |       |       |-- 1-yosys_4.stat.rpt
|   |   |       |       |-- 1-yosys_dff.stat
|   |   |       |       |-- 1-yosys_pre.stat
|   |   |       |       |-- 2-opensta.min_max.rpt
|   |   |       |       |-- 2-opensta.rpt
|   |   |       |       |-- 2-opensta.slew.rpt
|   |   |       |       |-- 2-opensta.timing.rpt
|   |   |       |       |-- 2-opensta_tns.rpt
|   |   |       |       `-- 2-opensta_wns.rpt
|   |   |       |-- results
|   |   |       |   |-- cts
|   |   |       |   |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |       |   |-- cvc
|   |   |       |   |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |       |   |-- floorplan
|   |   |       |   |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |       |   |-- klayout
|   |   |       |   |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |       |   |-- lvs
|   |   |       |   |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |       |   |-- magic
|   |   |       |   |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |       |   |-- placement
|   |   |       |   |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |       |   |-- routing
|   |   |       |   |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |       |   `-- synthesis
|   |   |       |       |-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |       |       `-- picorv32a.synthesis.v
|   |   |       `-- tmp
|   |   |           |-- cts
|   |   |           |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |           |-- cvc
|   |   |           |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |           |-- floorplan
|   |   |           |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |           |-- klayout
|   |   |           |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |           |-- lvs
|   |   |           |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |           |-- magic
|   |   |           |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |           |-- merged.lef
|   |   |           |-- merged_unpadded.lef
|   |   |           |-- met_layers_list.txt
|   |   |           |-- placement
|   |   |           |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |           |-- routing
|   |   |           |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |           |-- sky130_fd_sc_hd__tt_025C_1v80.no_pg.lib
|   |   |           |-- synthesis
|   |   |           |   |-- hierarchy.dot
|   |   |           |   |-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |           |   `-- yosys.sdc
|   |   |           |-- tracks_copy.info
|   |   |           |-- trimmed.lib
|   |   |           `-- trimmed.lib.exclude.list
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- picorv32a.sdc
|   |       `-- picorv32a.v
|   |-- point_add
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- ecg.v
|   |       `-- point_add.sdc
|   |-- point_scalar_mult
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- ecg.v
|   |       `-- point_scalar_mult.sdc
|   |-- s44
|   |   |-- config.tcl
|   |   |-- pdn.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- lut.v
|   |       `-- lut_s44.v
|   |-- salsa20
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- salsa20.sdc
|   |       `-- salsa20.v
|   |-- sha3
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- sha3.sdc
|   |       `-- sha3.v
|   |-- sha512
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- sha512.sdc
|   |       `-- sha512.v
|   |-- sound
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- dsp_dma_identification_rom.hex
|   |       |-- opl2_attack_rom.hex
|   |       |-- opl2_waveform_rom.hex
|   |       `-- sound.v
|   |-- spm
|   |   |-- config.json
|   |   |-- config.tcl
|   |   |-- pin_order.cfg
|   |   |-- runs
|   |   |   |-- 19-05_19-02
|   |   |   |   |-- OPENLANE_VERSION
|   |   |   |   |-- PDK_SOURCES
|   |   |   |   |-- cmds.log
|   |   |   |   |-- config.tcl
|   |   |   |   |-- logs
|   |   |   |   |   |-- 0-prep_runtime.txt
|   |   |   |   |   |-- 14-write_verilog.log
|   |   |   |   |   |-- 14-write_verilog_runtime.txt
|   |   |   |   |   |-- 16-write_verilog.log
|   |   |   |   |   |-- 16-write_verilog_runtime.txt
|   |   |   |   |   |-- 20-write_verilog.log
|   |   |   |   |   |-- 20-write_verilog_runtime.txt
|   |   |   |   |   |-- 26-write_verilog.log
|   |   |   |   |   |-- 26-write_verilog_runtime.txt
|   |   |   |   |   |-- 9-write_verilog.log
|   |   |   |   |   |-- 9-write_verilog_runtime.txt
|   |   |   |   |   |-- cts
|   |   |   |   |   |   |-- 13-cts.log
|   |   |   |   |   |   `-- 13-cts_runtime.txt
|   |   |   |   |   |-- cvc
|   |   |   |   |   |   |-- 42-cvc_runtime.txt
|   |   |   |   |   |   `-- 42-cvc_screen.log
|   |   |   |   |   |-- floorplan
|   |   |   |   |   |   |-- 3-verilog2def.openroad.log
|   |   |   |   |   |   |-- 3-verilog2def_openroad_runtime.txt
|   |   |   |   |   |   |-- 4-ioPlacer.log
|   |   |   |   |   |   |-- 4-ioPlacer_runtime.txt
|   |   |   |   |   |   |-- 5-tapcell.log
|   |   |   |   |   |   |-- 5-tapcell_runtime.txt
|   |   |   |   |   |   |-- 7-pdn.log
|   |   |   |   |   |   `-- 7-pdn_runtime.txt
|   |   |   |   |   |-- flow_summary.log
|   |   |   |   |   |-- klayout
|   |   |   |   |   |   |-- 12-klayout.scrot.log
|   |   |   |   |   |   |-- 12-klayout_scrot_runtime.txt
|   |   |   |   |   |   |-- 15-klayout.scrot.log
|   |   |   |   |   |   |-- 15-klayout_scrot_runtime.txt
|   |   |   |   |   |   |-- 22-klayout.scrot.log
|   |   |   |   |   |   |-- 22-klayout_scrot_runtime.txt
|   |   |   |   |   |   |-- 28-klayout.scrot.log
|   |   |   |   |   |   |-- 28-klayout_scrot_runtime.txt
|   |   |   |   |   |   |-- 32-klayout.log
|   |   |   |   |   |   |-- 32-klayout_runtime.txt
|   |   |   |   |   |   |-- 33-klayout.scrot.log
|   |   |   |   |   |   |-- 33-klayout_scrot_runtime.txt
|   |   |   |   |   |   |-- 34-klayout.xor.log
|   |   |   |   |   |   |-- 35-klayout.scrot.log
|   |   |   |   |   |   |-- 35-klayout_scrot_runtime.txt
|   |   |   |   |   |   |-- 36-klayout.xor.log
|   |   |   |   |   |   |-- 36-klayout_xor_runtime.txt
|   |   |   |   |   |   |-- 6-klayout.scrot.log
|   |   |   |   |   |   `-- 6-klayout_scrot_runtime.txt
|   |   |   |   |   |-- lvs
|   |   |   |   |   |   |-- 25-write_powered_verilog.log
|   |   |   |   |   |   |-- 38-lvs.lef.log
|   |   |   |   |   |   `-- 38-lvs_runtime.txt
|   |   |   |   |   |-- magic
|   |   |   |   |   |   |-- 27-magic.log
|   |   |   |   |   |   |-- 29-magic.mag.gds_ptrs.log
|   |   |   |   |   |   |-- 30-magic.lef.log
|   |   |   |   |   |   |-- 31-magic.maglef.log
|   |   |   |   |   |   |-- 31-magic_gen_runtime.txt
|   |   |   |   |   |   |-- 37-magic_ext2spice.feedback.txt
|   |   |   |   |   |   |-- 37-magic_ext_spice_runtime.txt
|   |   |   |   |   |   |-- 37-magic_spice.log
|   |   |   |   |   |   |-- 39-magic.drc.log
|   |   |   |   |   |   `-- 39-magic_drc_runtime.txt
|   |   |   |   |   |-- placement
|   |   |   |   |   |   |-- 11-opendp.log
|   |   |   |   |   |   |-- 11-opendp_runtime.txt
|   |   |   |   |   |   |-- 15-resizer_timing.log
|   |   |   |   |   |   |-- 15-resizer_timing_runtime.txt
|   |   |   |   |   |   |-- 8-replace.log
|   |   |   |   |   |   |-- 8-replace_runtime.txt
|   |   |   |   |   |   |-- 8-resizer.log
|   |   |   |   |   |   `-- 8-resizer_runtime.txt
|   |   |   |   |   |-- routing
|   |   |   |   |   |   |-- 18-fastroute.log
|   |   |   |   |   |   |-- 18-fastroute_runtime.txt
|   |   |   |   |   |   |-- 19-addspacers.log
|   |   |   |   |   |   |-- 19-addspacers_runtime.txt
|   |   |   |   |   |   |-- 21-tritonRoute.log
|   |   |   |   |   |   |-- 21-tritonRoute_runtime.txt
|   |   |   |   |   |   |-- 23-spef_extraction.log
|   |   |   |   |   |   |-- 23-spef_extraction_runtime.txt
|   |   |   |   |   |   |-- 40-or_antenna.log
|   |   |   |   |   |   |-- 41-or_antenna_runtime.txt
|   |   |   |   |   |   `-- fastroute.log
|   |   |   |   |   `-- synthesis
|   |   |   |   |       |-- 1-yosys.log
|   |   |   |   |       |-- 1-yosys_runtime.txt
|   |   |   |   |       |-- 10-opensta_post_resizer
|   |   |   |   |       |-- 10-opensta_post_resizer_runtime.txt
|   |   |   |   |       |-- 17-opensta_post_resizer_timing
|   |   |   |   |       |-- 17-opensta_post_resizer_timing_runtime.txt
|   |   |   |   |       |-- 2-opensta
|   |   |   |   |       |-- 2-opensta_runtime.txt
|   |   |   |   |       |-- 24-opensta_spef
|   |   |   |   |       `-- 24-opensta_spef_runtime.txt
|   |   |   |   |-- reports
|   |   |   |   |   |-- cts
|   |   |   |   |   |   |-- 13-cts.min_max.rpt
|   |   |   |   |   |   |-- 13-cts.rpt
|   |   |   |   |   |   |-- 13-cts.timing.rpt
|   |   |   |   |   |   |-- 13-cts_clock_skew.rpt
|   |   |   |   |   |   |-- 13-cts_tns.rpt
|   |   |   |   |   |   `-- 13-cts_wns.rpt
|   |   |   |   |   |-- cvc
|   |   |   |   |   |-- final_summary_report.csv
|   |   |   |   |   |-- floorplan
|   |   |   |   |   |   |-- 3-verilog2def.core_area.rpt
|   |   |   |   |   |   `-- 3-verilog2def.die_area.rpt
|   |   |   |   |   |-- klayout
|   |   |   |   |   |   |-- 34-klayout.xor.rpt
|   |   |   |   |   |   `-- 36-klayout.xor.rpt
|   |   |   |   |   |-- lvs
|   |   |   |   |   |-- magic
|   |   |   |   |   |   |-- 39-magic.drc
|   |   |   |   |   |   |-- 39-magic.drc.klayout.xml
|   |   |   |   |   |   |-- 39-magic.drc.rdb
|   |   |   |   |   |   |-- 39-magic.drc.tcl
|   |   |   |   |   |   `-- 39-magic.tr.drc
|   |   |   |   |   |-- manufacturability_report.rpt
|   |   |   |   |   |-- placement
|   |   |   |   |   |   |-- 8-replace.min_max.rpt
|   |   |   |   |   |   |-- 8-replace.rpt
|   |   |   |   |   |   |-- 8-replace.timing.rpt
|   |   |   |   |   |   |-- 8-replace_tns.rpt
|   |   |   |   |   |   `-- 8-replace_wns.rpt
|   |   |   |   |   |-- routed_runtime.txt
|   |   |   |   |   |-- routing
|   |   |   |   |   |   |-- 18-fastroute.min_max.rpt
|   |   |   |   |   |   |-- 18-fastroute.rpt
|   |   |   |   |   |   |-- 18-fastroute.timing.rpt
|   |   |   |   |   |   |-- 18-fastroute_tns.rpt
|   |   |   |   |   |   |-- 18-fastroute_wns.rpt
|   |   |   |   |   |   |-- 21-tritonRoute.drc
|   |   |   |   |   |   |-- 21-tritonRoute.klayout.xml
|   |   |   |   |   |   `-- 41-antenna.rpt
|   |   |   |   |   |-- runtime_summary_report.rpt
|   |   |   |   |   |-- runtime_summary_report.rpt.parsable
|   |   |   |   |   |-- synthesis
|   |   |   |   |   |   |-- 1-yosys_4.chk.rpt
|   |   |   |   |   |   |-- 1-yosys_4.stat.rpt
|   |   |   |   |   |   |-- 1-yosys_dff.stat
|   |   |   |   |   |   |-- 1-yosys_pre.stat
|   |   |   |   |   |   |-- 10-opensta_post_resizer.min_max.rpt
|   |   |   |   |   |   |-- 10-opensta_post_resizer.rpt
|   |   |   |   |   |   |-- 10-opensta_post_resizer.slew.rpt
|   |   |   |   |   |   |-- 10-opensta_post_resizer.timing.rpt
|   |   |   |   |   |   |-- 10-opensta_post_resizer_tns.rpt
|   |   |   |   |   |   |-- 10-opensta_post_resizer_wns.rpt
|   |   |   |   |   |   |-- 17-opensta_post_resizer_timing.min_max.rpt
|   |   |   |   |   |   |-- 17-opensta_post_resizer_timing.rpt
|   |   |   |   |   |   |-- 17-opensta_post_resizer_timing.slew.rpt
|   |   |   |   |   |   |-- 17-opensta_post_resizer_timing.timing.rpt
|   |   |   |   |   |   |-- 17-opensta_post_resizer_timing_tns.rpt
|   |   |   |   |   |   |-- 17-opensta_post_resizer_timing_wns.rpt
|   |   |   |   |   |   |-- 2-opensta.min_max.rpt
|   |   |   |   |   |   |-- 2-opensta.rpt
|   |   |   |   |   |   |-- 2-opensta.slew.rpt
|   |   |   |   |   |   |-- 2-opensta.timing.rpt
|   |   |   |   |   |   |-- 2-opensta_tns.rpt
|   |   |   |   |   |   |-- 2-opensta_wns.rpt
|   |   |   |   |   |   |-- 24-opensta_spef.min_max.rpt
|   |   |   |   |   |   |-- 24-opensta_spef.rpt
|   |   |   |   |   |   |-- 24-opensta_spef.slew.rpt
|   |   |   |   |   |   |-- 24-opensta_spef.timing.rpt
|   |   |   |   |   |   |-- 24-opensta_spef_tns.rpt
|   |   |   |   |   |   `-- 24-opensta_spef_wns.rpt
|   |   |   |   |   `-- total_runtime.txt
|   |   |   |   |-- results
|   |   |   |   |   |-- cts
|   |   |   |   |   |   |-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |   |   |   |-- spm.cts.def
|   |   |   |   |   |   `-- spm.cts.def.png
|   |   |   |   |   |-- cvc
|   |   |   |   |   |   |-- cvc_spm.debug.gz
|   |   |   |   |   |   |-- cvc_spm.error.gz
|   |   |   |   |   |   |-- cvc_spm.log
|   |   |   |   |   |   |-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |   |   |   |-- spm.cdl
|   |   |   |   |   |   `-- spm.power
|   |   |   |   |   |-- floorplan
|   |   |   |   |   |   |-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |   |   |   |-- spm.floorplan.def
|   |   |   |   |   |   `-- spm.floorplan.def.png
|   |   |   |   |   |-- klayout
|   |   |   |   |   |   |-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |   |   |   |-- spm.gds
|   |   |   |   |   |   |-- spm.gds.png
|   |   |   |   |   |   |-- spm.lyp
|   |   |   |   |   |   |-- spm.xor.gds
|   |   |   |   |   |   |-- spm.xor.gds.png
|   |   |   |   |   |   `-- spm.xor.xml
|   |   |   |   |   |-- lvs
|   |   |   |   |   |   |-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |   |   |   |-- spm.lvs.lef.json
|   |   |   |   |   |   |-- spm.lvs.lef.log
|   |   |   |   |   |   |-- spm.lvs.powered.v
|   |   |   |   |   |   `-- spm.lvs_parsed.lef.log
|   |   |   |   |   |-- magic
|   |   |   |   |   |   |-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |   |   |   |-- spm.drc.mag
|   |   |   |   |   |   |-- spm.gds
|   |   |   |   |   |   |-- spm.gds.png
|   |   |   |   |   |   |-- spm.lef
|   |   |   |   |   |   |-- spm.lef.mag
|   |   |   |   |   |   |-- spm.lef.spice
|   |   |   |   |   |   |-- spm.mag
|   |   |   |   |   |   `-- spm.spice
|   |   |   |   |   |-- placement
|   |   |   |   |   |   |-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |   |   |   |-- spm.placement.def
|   |   |   |   |   |   `-- spm.placement.def.png
|   |   |   |   |   |-- routing
|   |   |   |   |   |   |-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |   |   |   |-- spm.def
|   |   |   |   |   |   |-- spm.def.png
|   |   |   |   |   |   |-- spm.def.ref
|   |   |   |   |   |   `-- spm.spef
|   |   |   |   |   `-- synthesis
|   |   |   |   |       |-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |   |       |-- spm.synthesis.v
|   |   |   |   |       |-- spm.synthesis_cts.v
|   |   |   |   |       |-- spm.synthesis_optimized.v
|   |   |   |   |       `-- spm.synthesis_preroute.v
|   |   |   |   `-- tmp
|   |   |   |       |-- cts
|   |   |   |       |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |       |-- cts.lib
|   |   |   |       |-- cts.lib.exclude.list
|   |   |   |       |-- cvc
|   |   |   |       |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |       |-- floorplan
|   |   |   |       |   |-- 3-verilog2def_openroad.def
|   |   |   |       |   |-- 4-ioPlacer.def
|   |   |   |       |   |-- 7-pdn.def
|   |   |   |       |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |       |-- klayout
|   |   |   |       |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |       |-- lvs
|   |   |   |       |   |-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |       |   `-- setup_file.lef.lvs
|   |   |   |       |-- magic
|   |   |   |       |   |-- magic_gds_ptrs.mag
|   |   |   |       |   |-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |       |   |-- sky130_fd_sc_hd__a21oi_2.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__a22o_1.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__a31oi_1.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__and2_1.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__buf_1.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__clkbuf_1.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__clkbuf_16.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__clkbuf_2.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__decap_12.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__decap_3.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__decap_4.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__decap_6.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__decap_8.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__dfrtp_1.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__dlymetal6s2s_1.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__fill_1.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__fill_2.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__inv_2.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__o2bb2a_1.ext
|   |   |   |       |   |-- sky130_fd_sc_hd__tapvpwrvgnd_1.ext
|   |   |   |       |   `-- spm.ext
|   |   |   |       |-- magic_spice.tcl
|   |   |   |       |-- merged.lef
|   |   |   |       |-- merged_unpadded.lef
|   |   |   |       |-- met_layers_list.txt
|   |   |   |       |-- placement
|   |   |   |       |   |-- 15-resizer_timing.def
|   |   |   |       |   |-- 8-replace.def
|   |   |   |       |   |-- 8-resizer.def
|   |   |   |       |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |       |-- resizer.lib
|   |   |   |       |-- resizer.lib.exclude.list
|   |   |   |       |-- routing
|   |   |   |       |   |-- 18-fastroute.def
|   |   |   |       |   |-- 18-fastroute.guide
|   |   |   |       |   |-- 19-addspacers.def
|   |   |   |       |   |-- 21-tritonRoute.guide
|   |   |   |       |   |-- 21-tritonRoute.param
|   |   |   |       |   |-- 21-tritonRoute_TA.def
|   |   |   |       |   |-- 25-spm.powered.def
|   |   |   |       |   `-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |       |-- sky130_fd_sc_hd__tt_025C_1v80.no_pg.lib
|   |   |   |       |-- synthesis
|   |   |   |       |   |-- hierarchy.dot
|   |   |   |       |   |-- merged_unpadded.lef -> ../../tmp/merged_unpadded.lef
|   |   |   |       |   `-- yosys.sdc
|   |   |   |       |-- tracks_copy.info
|   |   |   |       |-- trimmed.lib
|   |   |   |       `-- trimmed.lib.exclude.list
|   |   |   `-- 29-06_07-34
|   |   |       |-- OPENLANE_VERSION
|   |   |       |-- PDK_SOURCES
|   |   |       |-- cmds.log
|   |   |       |-- config.tcl
|   |   |       |-- logs
|   |   |       |   |-- 0-prep_runtime.txt
|   |   |       |   |-- cts
|   |   |       |   |-- cvc
|   |   |       |   |-- floorplan
|   |   |       |   |   |-- 3-verilog2def.openroad.log
|   |   |       |   |   |-- 3-verilog2def_openroad_runtime.txt
|   |   |       |   |   |-- 4-ioPlacer.log
|   |   |       |   |   |-- 4-ioPlacer_runtime.txt
|   |   |       |   |   |-- 5-tapcell.log
|   |   |       |   |   |-- 5-tapcell_runtime.txt
|   |   |       |   |   |-- 7-pdn.log
|   |   |       |   |   `-- 7-pdn_runtime.txt
|   |   |       |   |-- flow_summary.log
|   |   |       |   |-- klayout
|   |   |       |   |   |-- 6-klayout.scrot.log
|   |   |       |   |   `-- 6-klayout_scrot_runtime.txt
|   |   |       |   |-- lvs
|   |   |       |   |-- magic
|   |   |       |   |-- placement
|   |   |       |   |-- routing
|   |   |       |   `-- synthesis
|   |   |       |       |-- 1-yosys.log
|   |   |       |       |-- 1-yosys_runtime.txt
|   |   |       |       |-- 2-opensta
|   |   |       |       `-- 2-opensta_runtime.txt
|   |   |       |-- reports
|   |   |       |   |-- cts
|   |   |       |   |-- cvc
|   |   |       |   |-- floorplan
|   |   |       |   |   |-- 3-verilog2def.core_area.rpt
|   |   |       |   |   `-- 3-verilog2def.die_area.rpt
|   |   |       |   |-- klayout
|   |   |       |   |-- lvs
|   |   |       |   |-- magic
|   |   |       |   |-- placement
|   |   |       |   |-- routing
|   |   |       |   `-- synthesis
|   |   |       |       |-- 1-yosys_4.chk.rpt
|   |   |       |       |-- 1-yosys_4.stat.rpt
|   |   |       |       |-- 1-yosys_dff.stat
|   |   |       |       |-- 1-yosys_pre.stat
|   |   |       |       |-- 2-opensta.min_max.rpt
|   |   |       |       |-- 2-opensta.rpt
|   |   |       |       |-- 2-opensta.slew.rpt
|   |   |       |       |-- 2-opensta.timing.rpt
|   |   |       |       |-- 2-opensta_tns.rpt
|   |   |       |       `-- 2-opensta_wns.rpt
|   |   |       |-- results
|   |   |       |   |-- cts
|   |   |       |   |   `-- merged_unpadded.lef
|   |   |       |   |-- cvc
|   |   |       |   |   `-- merged_unpadded.lef
|   |   |       |   |-- floorplan
|   |   |       |   |   |-- merged_unpadded.lef
|   |   |       |   |   |-- spm.floorplan.def
|   |   |       |   |   `-- spm.floorplan.def.png
|   |   |       |   |-- klayout
|   |   |       |   |   `-- merged_unpadded.lef
|   |   |       |   |-- lvs
|   |   |       |   |   `-- merged_unpadded.lef
|   |   |       |   |-- magic
|   |   |       |   |   `-- merged_unpadded.lef
|   |   |       |   |-- placement
|   |   |       |   |   `-- merged_unpadded.lef
|   |   |       |   |-- routing
|   |   |       |   |   `-- merged_unpadded.lef
|   |   |       |   `-- synthesis
|   |   |       |       |-- merged_unpadded.lef
|   |   |       |       `-- spm.synthesis.v
|   |   |       `-- tmp
|   |   |           |-- cts
|   |   |           |   `-- merged_unpadded.lef
|   |   |           |-- cvc
|   |   |           |   `-- merged_unpadded.lef
|   |   |           |-- floorplan
|   |   |           |   |-- 3-verilog2def_openroad.def
|   |   |           |   |-- 4-ioPlacer.def
|   |   |           |   |-- 7-pdn.def
|   |   |           |   `-- merged_unpadded.lef
|   |   |           |-- klayout
|   |   |           |   `-- merged_unpadded.lef
|   |   |           |-- lvs
|   |   |           |   `-- merged_unpadded.lef
|   |   |           |-- magic
|   |   |           |   `-- merged_unpadded.lef
|   |   |           |-- merged.lef
|   |   |           |-- merged_unpadded.lef
|   |   |           |-- met_layers_list.txt
|   |   |           |-- placement
|   |   |           |   `-- merged_unpadded.lef
|   |   |           |-- routing
|   |   |           |   `-- merged_unpadded.lef
|   |   |           |-- sky130_fd_sc_hd__tt_025C_1v80.no_pg.lib
|   |   |           |-- synthesis
|   |   |           |   |-- hierarchy.dot
|   |   |           |   |-- merged_unpadded.lef
|   |   |           |   `-- yosys.sdc
|   |   |           |-- tracks_copy.info
|   |   |           |-- trimmed.lib
|   |   |           `-- trimmed.lib.exclude.list
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- spm.sdc
|   |       `-- spm.v
|   |-- synth_ram
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       `-- synth_ram.v
|   |-- usb
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       `-- usb2p0_core.v
|   |-- usb_cdc_core
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- usb_cdc_core.sdc
|   |       |-- usb_cdc_core.v
|   |       |-- usb_desc_rom.v
|   |       |-- usbf_crc16.v
|   |       |-- usbf_defs.v
|   |       |-- usbf_device_core.v
|   |       |-- usbf_sie_rx.v
|   |       `-- usbf_sie_tx.v
|   |-- usbf_device
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       `-- usbf_device.v
|   |-- wbqspiflash
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- wbqspiflash.sdc
|   |       `-- wbqspiflash.v
|   |-- xtea
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- xtea.sdc
|   |       `-- xtea.v
|   |-- y_dct
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- y_dct.sdc
|   |       `-- y_dct.v
|   |-- y_huff
|   |   |-- config.tcl
|   |   |-- sky130A_sky130_fd_sc_hd_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hdll_config.tcl
|   |   |-- sky130A_sky130_fd_sc_hs_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ls_config.tcl
|   |   |-- sky130A_sky130_fd_sc_ms_config.tcl
|   |   `-- src
|   |       |-- y_huff.sdc
|   |       `-- y_huff.v
|   `-- zipdiv
|       |-- config.tcl
|       |-- sky130A_sky130_fd_sc_hd_config.tcl
|       |-- sky130A_sky130_fd_sc_hdll_config.tcl
|       |-- sky130A_sky130_fd_sc_hs_config.tcl
|       |-- sky130A_sky130_fd_sc_ls_config.tcl
|       |-- sky130A_sky130_fd_sc_ms_config.tcl
|       `-- src
|           |-- zipdiv.sdc
|           `-- zipdiv.v
|-- docker_build
|   |-- Dockerfile
|   |-- Makefile
|   |-- README.md
|   |-- docker
|   |   |-- antmicro_yosys
|   |   |   `-- Dockerfile
|   |   |-- cugr
|   |   |   `-- Dockerfile
|   |   |-- cvc
|   |   |   |-- Dockerfile
|   |   |   `-- cvc-1.0.0.tar.gz
|   |   |-- drcu
|   |   |   `-- Dockerfile
|   |   |-- klayout
|   |   |   `-- Dockerfile
|   |   |-- magic
|   |   |   `-- Dockerfile
|   |   |-- netgen
|   |   |   `-- Dockerfile
|   |   |-- opendp
|   |   |   `-- Dockerfile
|   |   |-- openphysyn
|   |   |   `-- Dockerfile
|   |   |-- openroad_app
|   |   |   |-- Dockerfile
|   |   |   |-- ignore_obs_outside.patch
|   |   |   |-- opendp-diamond-search.patch
|   |   |   |-- pdn_gen_core_ring_fix.patch
|   |   |   |-- pdngen_export_subst.patch
|   |   |   |-- rails.patch
|   |   |   `-- setup_local.patch
|   |   |-- opensta
|   |   |   `-- Dockerfile
|   |   |-- padring
|   |   |   `-- Dockerfile
|   |   |-- replace
|   |   |   `-- Dockerfile
|   |   |-- route
|   |   |   `-- Dockerfile
|   |   |-- vlogtoverilog
|   |   |   `-- Dockerfile
|   |   `-- yosys
|   |       `-- Dockerfile
|   |-- hooks
|   |   `-- build
|   `-- tar
|       |-- antmicro_yosys.tar.gz
|       |-- cugr.tar.gz
|       |-- cvc.tar.gz
|       |-- drcu.tar.gz
|       |-- klayout.tar.gz
|       |-- magic.tar.gz
|       |-- netgen.tar.gz
|       |-- opendp.tar.gz
|       |-- openphysyn.tar.gz
|       |-- openroad_app.tar.gz
|       |-- opensta.tar.gz
|       |-- padring.tar.gz
|       |-- replace.tar.gz
|       |-- route.tar.gz
|       |-- vlogtoverilog.tar.gz
|       `-- yosys.tar.gz
|-- docs
|   |-- Makefile
|   |-- _ext
|   |   |-- image_links.py
|   |   |-- markdown_code_links.py
|   |   |-- markdown_cross_doc_section_links.py
|   |   `-- toc_from_markdown.py
|   |-- _static
|   |   |-- openlane.flow.1.png
|   |   `-- striVe.jpeg
|   |-- environment.yml
|   |-- requirements.txt
|   `-- source
|       |-- Manual_PDK_installation.md
|       |-- OpenLANE_commands.md
|       |-- PDK_STRUCTURE.md
|       |-- advanced_power_grid_control.md
|       |-- advanced_readme.md
|       |-- chip_integration.md
|       `-- hardening_macros.md
|-- flow.tcl
|-- regression_results
|   |-- README.md
|   |-- benchmark_results
|   |   |-- SW_HD.csv
|   |   |-- SW_HD.html
|   |   |-- SW_HDLL.csv
|   |   |-- SW_HDLL.html
|   |   |-- SW_HS.csv
|   |   |-- SW_HS.html
|   |   |-- SW_LS.csv
|   |   |-- SW_LS.html
|   |   |-- SW_MS.csv
|   |   `-- SW_MS.html
|   `-- columns_defintions.md
|-- report_generation_wrapper.py
|-- run_designs.py
`-- scripts
    |-- add_def_obstructions.py
    |-- append_special_nets.py
    |-- apply_def_template.py
    |-- base.sdc
    |-- cleanupConfigs.py
    |-- compare_regression_design.py
    |-- compare_regression_reports.py
    |-- config
    |   |-- __pycache__
    |   |   `-- config.cpython-36.pyc
    |   |-- config.py
    |   |-- config_get.sh
    |   |-- generate_config.py
    |   |-- generate_config.sh
    |   `-- regression.config
    |-- consoletext.py
    |-- contextualize.py
    |-- count_lvs.py
    |-- csv2html
    |   |-- csv2html.py
    |   |-- static
    |   |   `-- style.css
    |   `-- templates
    |       |-- _partial.html
    |       `-- main.html
    |-- cts
    |   `-- cts_simple.pl
    |-- cvc
    |   `-- sky130A
    |       |-- cvc.sky130A.models
    |       `-- cvcrc.sky130A
    |-- expand_diearea.sh
    |-- extract_antenna_violators.py
    |-- extract_coreinfo.sh
    |-- extract_metal_layers.py
    |-- fakeDiodeReplace.py
    |-- fixlayernames.sh
    |-- gds2lef.py
    |-- get_core_dimensions.py
    |-- grepCount.sh
    |-- io_place.py
    |-- klayout
    |   |-- def2gds.py
    |   |-- def2gds.sh
    |   |-- mv_shapes.py
    |   |-- mv_shapes.sh
    |   |-- run_drc.sh
    |   |-- scrotLayout.py
    |   |-- scrotLayout.sh
    |   |-- xor.drc
    |   `-- xor.sh
    |-- label_macro_pins.py
    |-- label_padframe.py
    |-- lef_copy_annotation.py
    |-- lef_enforce_manufacturing_grid.py
    |-- li1_hack_end.py
    |-- li1_hack_start.py
    |-- libtrim.pl
    |-- logic_equiv_check.tcl
    |-- magic
    |   |-- drc.tcl
    |   |-- drc_batch.tcl
    |   |-- erase_box.sh
    |   |-- gds_pointers.tcl
    |   |-- gdses2mags.tcl
    |   |-- lef.tcl
    |   |-- lefs2maglefs.tcl
    |   |-- mag.tcl
    |   |-- mag_gds.tcl
    |   `-- maglef.tcl
    |-- magic_drc_to_rdb.py
    |-- magic_drc_to_tcl.py
    |-- magic_drc_to_tr_drc.py
    |-- manual_macro_place.py
    |-- mark_component_fixed.sh
    |-- mergeLef.py
    |-- merge_components.sh
    |-- mv_components.sh
    |-- mv_pins.sh
    |-- obs.py
    |-- obs_above.py
    |-- openPhySyn.tcl
    |-- openroad
    |   |-- or_antenna_check.tcl
    |   |-- or_basic_mp.tcl
    |   |-- or_cts.tcl
    |   |-- or_diodes.tcl
    |   |-- or_droute.tcl
    |   |-- or_fill.tcl
    |   |-- or_floorplan.tcl
    |   |-- or_groute.tcl
    |   |-- or_ioplacer.tcl
    |   |-- or_opendp.tcl
    |   |-- or_pdn.tcl
    |   |-- or_replace.tcl
    |   |-- or_resizer.tcl
    |   |-- or_resizer_timing.tcl
    |   |-- or_tapcell.tcl
    |   `-- or_write_verilog.tcl
    |-- padLefMacro.py
    |-- padframe2fp.py
    |-- padframe_extract_area.sh
    |-- padringer.py
    |-- parse_klayout_xor_log.py
    |-- pfg.py
    |-- place_diodes.py
    |-- power_route.py
    |-- random_place.py
    |-- rectify.py
    |-- rectify_above.py
    |-- removeEnvVar.sh
    |-- remove_components.sh
    |-- remove_def_component.sh
    |-- remove_empty_nets.sh
    |-- remove_empty_pins.py
    |-- remove_empty_ports.py
    |-- remove_nets.sh
    |-- remove_pins.sh
    |-- replace_gp.tcl
    |-- replace_prefix_from_def_instances.py
    |-- replicateDesignsConfigs.py
    |-- report
    |   |-- __pycache__
    |   |   |-- get_file_name.cpython-36.pyc
    |   |   `-- report.cpython-36.pyc
    |   |-- get_best.py
    |   |-- get_file_name.py
    |   |-- report.py
    |   `-- report.sh
    |-- setLayerTracks.py
    |-- spef_extractor
    |   |-- LICENSE
    |   |-- README.md
    |   |-- lef_def_parser
    |   |   |-- LICENSE
    |   |   |-- __init__.py
    |   |   |-- __pycache__
    |   |   |   |-- __init__.cpython-36.pyc
    |   |   |   |-- def_parser.cpython-36.pyc
    |   |   |   |-- def_util.cpython-36.pyc
    |   |   |   |-- lef_parser.cpython-36.pyc
    |   |   |   |-- lef_util.cpython-36.pyc
    |   |   |   `-- util.cpython-36.pyc
    |   |   |-- def_parser.py
    |   |   |-- def_util.py
    |   |   |-- lef_parser.py
    |   |   |-- lef_util.py
    |   |   `-- util.py
    |   `-- main.py
    |-- sta.tcl
    |-- synth.tcl
    |-- synth_exp
    |   |-- analyze.pl
    |   |-- table.css
    |   `-- utils.js
    |-- synth_top.tcl
    |-- tcl_commands
    |   |-- README.md
    |   |-- all.tcl
    |   |-- checkers.tcl
    |   |-- cts.tcl
    |   |-- cvc.tcl
    |   |-- floorplan.tcl
    |   |-- init_design.tcl
    |   |-- klayout.tcl
    |   |-- list.txt
    |   |-- lvs.tcl
    |   |-- magic.tcl
    |   |-- pkgIndex.tcl
    |   |-- placement.tcl
    |   |-- refresh.tcl
    |   |-- routing.tcl
    |   `-- synthesis.tcl
    |-- tksimpledialog.py
    |-- topModuleGen
    |   |-- README.md
    |   `-- src
    |       |-- TopModuleGen.py
    |       `-- padHelper.py
    |-- tr2klayout.py
    |-- tritonRoute.param
    |-- unroller.sh
    |-- updateDesignsConfigs.py
    |-- utils
    |   |-- __init__.py
    |   |-- __pycache__
    |   |   |-- __init__.cpython-36.pyc
    |   |   `-- utils.cpython-36.pyc
    |   |-- deflef_utils.tcl
    |   |-- fake_display_buffer.tcl
    |   |-- pkgIndex.tcl
    |   |-- utils.py
    |   `-- utils.tcl
    |-- widenSiteLef.py
    |-- wrap_lef_macro.py
    |-- write_powered_def.py
    |-- yosys_rewrite_verilog.tcl
    |-- zeroize_origin_def.py
    `-- zeroize_origin_lef.py
```
