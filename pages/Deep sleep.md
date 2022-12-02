- ```C++
  void SysHandlenSLPSUS()
  {
      if (GPIO_RD(nSIO_SLP_SUS))
      {
          GPIO_WR(PCIAUX_CTRL, 1);
          GPIO_WR(RTL_LAN_POWER_CTRL, 1);
          GPIO_WR(nM2_WLAN_POWER_CTRL, 0);
          GPIO_WR (BC12_CTL3, 1);
          GPIO_WR(nSUS3V_ON, 0);
          // Back from deep, check PD pin status and send event if needed
          // byte checking_port_index;    //test_?
          // for(checking_port_index = 0; checking_port_index < SYS_MAX_UPD_PORTS; checking_port_index++) //test_?
          // {
          //     UPD_CheckUpdPortAlertIsr(checking_port_index);
          // }
      }
      else
      {
          GPIO_WR(PCIAUX_CTRL, 0);
          GPIO_WR(RTL_LAN_POWER_CTRL, 0);
          GPIO_WR(nM2_WLAN_POWER_CTRL, 1);
          GPIO_WR (BC12_CTL3, 0);
          GPIO_WR(nSUS3V_ON, 1);
      }
  }
  ```