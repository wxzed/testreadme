# DFRobot_BNO055 Intelligent 10DOF AHRS

The BNO055 is a System in Package (SiP), integrating a triaxial 14-bit accelerometer, 
a triaxial 16-bit gyroscope with a range of ±2000 degrees per second, a triaxial geomagnetic sensor 
and a 32-bit cortex M0+ microcontroller running Bosch Sensortec sensor fusion software, in a single package. 


## DFRobot_BNO055 Library for Arduino
---------------------------------------------------------
Provides an Arduino library for reading and interpreting Bosch BNO055 data over I2C.Used to read the current pose and calculate the Euler angles.

## Table of Contents

* [Installation](#installation)
* [Methods](#methods)
* [Compatibility](#compatibility)
* [History](#history)
* [Credits](#credits)

<snippet>
<content>

## Installation

To use this library download the zip file, uncompress it to a folder named DFRobot_BNO055. 
Download the zip file first to use this library and uncompress it to a folder named DFRobot_BNO055. 

## Methods

```C++

#if (ARDUINO >= 100)
 #include "Arduino.h"
#else
 #include "WProgram.h"
#endif
#include "Wire.h"

#define BNO055_ADDRESS                (0x28)        /* 0x28 com3 low 0x29 com3 high     */
#define BNO055_POLL_TIMEOUT           (100)         /* Maximum number of read attempts  */
#define BNO055_ID                     (0xA0)        /* pg58                             */

/*
 * @brief init BNO055 device
 *
 * @return result
 *    ture : falid
 *    false : succussful
 */
    bool init();
/*
 * @brief start read euler angles
 */
    void readEuler(void);
/*
 * @brief get system status information from BNO055
 */
    void getInfo(void);
/*
 * @brief read linear acceleration
 */
    void readLinAcc(void);
/*
 * @brief read quaternion data
 */
    void readQua(void);
/*
 * @brief uses last loaded QuaData and LinAccData.  ie, make sure reads for those have been called... 
 */
    void calcAbsLinAcc(void);
    
    byte SystemStatusCode;
    byte SelfTestStatus;
    byte SystemError;
    
    typedef enum
    {
        eNORMAL_POWER_MODE     = 0b00000000,
        eLOW_POWER_MODE        = 0b00000001,
        eSUSPEND_POWER_MODE    = 0b00000010,
    } eBNO055PowerModes_t;
    
    typedef enum
    {
        eFASTEST_MODE    = 0b00100000,
        eGAME_MODE       = 0b01000000,
        eUI_MODE         = 0b01100000,
        eNORMAL_MODE     = 0b10000000,
    } eBNO055DataRateMode_t;

    typedef struct BNO055EulerData_s
    {
      float x;
      float y;
      float z;
    } BNO055EulerData;
    
    typedef struct BNO055LinAccData_s
    {
        float x;
        float y;
        float z;
    } BNO055LinAccData;
    
    typedef struct BNO055QuaData_s
    {
        float w;
        float x;
        float y;
        float z;
    } BNO055QuaData;
    
    typedef struct BNO055AbsLinAccData_s
    {
        float x;
        float y;
        float z;
    } BNO055AbsLinAccData;

    BNO055EulerData EulerAngles;
    BNO055LinAccData LinAccData;
    BNO055QuaData QuaData;
    BNO055AbsLinAccData AbsLinAccData;


```

## Compatibility

MCU                | Work Well | Work Wrong | Untested  | Remarks
------------------ | :----------: | :----------: | :---------: | -----
FireBeetle-ESP32  |      √       |             |            | 
FireBeetle-ESP8266  |      √       |             |            | 
Arduino uno |       √      |             |            | 

## History

- Nov 31, 2018 - Version 0.1 released.

## Credits

Written by DFRobot_YangYue, 2018. (Welcome to our [website](https://www.dfrobot.com/))
