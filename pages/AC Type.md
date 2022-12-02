- 參數
	- hw_ACAVIN_NB 硬體adapter PSID interrupt
	- AC_TYPE 瓦數
-
- NB
	- 接上PSID
		- REGISTER_FOR_MESSAGE_EVENT(prvAcavHandleTask, MESSAGE_EVT_hw_ACAVIN_NB, (HandleAcavInNbChange))
- DT
	- adapter.cif
	- ```C++
	  REGISTER_FOR_MESSAGE_EVENT(prvAcavHandleTask, MESSAGE_EVT_SERVICE_2ND_AC_OCP, (PSIDSecondOCP))  
	  REGISTER_FOR_MESSAGE_EVENT(prvAcavHandleTask, MESSAGE_EVT_SERVICE_PSU, (HandlePSUAdapterPSID))  
	  REGISTER_FOR_MESSAGE_EVENT(prvAcavHandleTask, MESSAGE_EVT_S5_INIT, (HandlePSUAdapterPSID))  
	  ```
-
- ```C++
  void SysBarrelStatusCheck()
  {
      if(!ACAV_SW_NB && (ACAV_SW_NB != ACAV_IN_NB))
          SIGNAL_MESSAGE_EVENT_ONCE(MESSAGE_EVT_SERVICE_AC_TYPE, NULL);
  }
  
  VCI_OVRD_IN                                 hw_ACAV_IN              GPIO,IN
  GPIO060/KBRST/TST_CLK_OUT                   hw_ACAVIN_NB            GPIO,IN,EE
  ACAV_SW = hw_ACAV_IN;
  define ACAV_IN hw_ACAV_IN
  ACAV_SW_IN = ACAV_IN;
  ACAV_SW_NB = handle_ac_detection
  
  
  #define ACAV_IN hw_ACAV_IN
  
  判斷供電PSID能否使用(差入狀態
  DT:默認1
  NB:hw_ACAVIN_NB init
  #define ACAV_IN_NB		   sw_ACAV_IN_NB()
  
  #define WAKE_ACAV_FLAGS    WAKE_ACAV_STATE.ALLBITS
  
  // set if ACAV_IN_xx != ACAV_SW or acav_debounce()
  #define WAKE_ACAV          WAKE_ACAV_STATE.BITS.b0
  
  // macro to use for wake event registration
  #define WAKE_ACAV_ARG      &WAKE_ACAV_STATE.ALLBITS, 0
  
  // set if ACAV_IN_NB != ACAV_SW_NB
  #define WAKE_ACAV_NB       WAKE_ACAV_STATE.BITS.b1
  
  // set if ACAV_IN_DOCK != ACAV_SW_DOCK
  #define WAKE_ACAV_DOCK     WAKE_ACAV_STATE.BITS.b2
  
  // set if ACAV_IN_UPD != ACAV_SW_UPD
  #define WAKE_ACAV_UPD      WAKE_ACAV_STATE.BITS.b3
  
  // ACAV_IN debounced version
  #define ACAV_SW_IN    ACAV_SW_STATE.b1
  
  // ACAV_IN_NB debounced version
  #define ACAV_SW_NB    ACAV_SW_STATE.b2
  
  // ACAV_IN_DOCK debounced version
  #define ACAV_SW_DOCK  ACAV_SW_STATE.b3
  
  // NB Adapter is the primary adapter.
  #define PRIMARY_AC    ACAV_SW_STATE.b4
  ```
-
-
-