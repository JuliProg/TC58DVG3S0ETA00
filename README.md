![Create new chip](https://github.com/JuliProg/TC58DVG3S0ETA00/workflows/Create%20new%20chip/badge.svg?event=repository_dispatch)
![ChipUpdate](https://github.com/JuliProg/TC58DVG3S0ETA00/workflows/ChipUpdate/badge.svg)
# Join the development of the project ([list of tasks](https://github.com/users/JuliProg/projects/1))


# TC58DVG3S0ETA00
Implementation of the TC58DVG3S0ETA00 chip for the JuliProg programmer

Dependency injection, DI based on MEF framework is used to connect the chip to the programmer.

<section class = "listing">

# Chip parameters
```c#


        //--------------------Vendor Specific Pin configuration---------------------------

        //  VSP1(38pin) - NC    
        //  VSP2(35pin) - NC
        //  VSP3(20pin) - NC

        ChipAssembly()
        {
            myChip.devManuf = "TOSHIBA";
            myChip.name = "TC58DVG3S0ETA00";
            myChip.chipID = "98D390267614";      // device ID - 98h D1h 90h 15h 76h 14h

            myChip.width = Organization.x8;    // chip width - 8 bit
            myChip.bytesPP = 4096;             // page size - 4096 byte (4Kb)
            myChip.spareBytesPP = 218;          // size Spare Area - 218 byte
            myChip.pagesPB = 64;               // the number of pages per block - 64 
            myChip.bloksPLUN = 4096;           // number of blocks in CE - 4096
            myChip.LUNs = 1;                   // the amount of CE in the chip
            myChip.colAdrCycles = 2;           // cycles for column addressing
            myChip.rowAdrCycles = 3;           // cycles for row addressing 
            myChip.vcc = Vcc.v3_3;             // supply voltage
            (myChip as ChipPrototype_v1).EccBits = 1;                // required Ecc bits for each 512 bytes

```
# Chip operations
```c#


            //------- Add chip operations   https://github.com/JuliProg/Wiki#command-set---------------------------------------------------

            myChip.Operations("Reset_FFh").
                   Operations("Erase_60h_D0h").
                   Operations("Read_00h_30h").
                   Operations("PageProgram_80h_10h");

```
# Chip registers (optional)
```c#


            //------- Add chip registers (optional)----------------------------------------------------

            myChip.registers.Add(                   // https://github.com/JuliProg/Wiki/wiki/StatusRegister
                "Status Register").
                Size(1).
                Operations("ReadStatus_70h").
                Interpretation("SR_Interpreted").   
                UseAsStatusRegister();



            myChip.registers.Add(                  // https://github.com/JuliProg/Wiki/wiki/ID-Register
                "Id Register").
                Size(5).
                Operations("ReadId_90h");               
                //Interpretation(ID_interpreting);          

```
# Interpretation of ID-register values ​​(optional)
```c#


        public string ID_interpreting(Register register)   
        
```
</section>
















