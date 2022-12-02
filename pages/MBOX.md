- ## Common
- LED color
- #+BEGIN_PINNED
  MBOX[0] = 0xF8
   #+END_PINNED
-
-
-
- ## Property service
  PropertyServices.h
  #+BEGIN_TIP
  MBOX[0] = 0x1C //#define KB_PROPERTY_SERVICES
  PropertyServicesEvent.Command = MBOX[2];
  PropertyServicesEvent.PropertyId = ((MBOX[6] << 24) | (MBOX[5] << 16) | (MBOX[4] << 8) | MBOX[3]);
  PropertyServicesEvent.Length = MBOX[7];
  PropertyServicesEvent.Data = (byte *) &MBOX[8];
  #+END_TIP
-
- BIOS set model ID
- #+BEGIN_PINNED
  MBOX[0] = 0x1C
  MBOX[2] = 0x01
  0x0E34
  MBOX[3] = 0x34
  MBOX[4] = 0x0E
  MBOX[8] = model id
   #+END_PINNED
- advance debug mode
  id:: 6311d4a7-137e-41ff-80e0-e8d7b882ab2a
  #+BEGIN_PINNED
  MBOX[2] = 0x01
  
  0x0759
  MBOX[3] = 0x59
  MBOX[4] = 0x07
  
  MBOX[8] = 0x01
   #+END_PINNED
	-
-
-
-
	-