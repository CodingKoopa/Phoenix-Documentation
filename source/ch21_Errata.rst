.. _Errata:

Errata
======
.. _Errata-hero:

HERO firmware compatibility with firmware 4.X
--------------------------------------------------------
The HERO robot controller still requires 11.X firmware in the motor controllers to function correctly.
This will addressed in a future release (which updates HERO).

No S-Curve VI in LabVIEW
-----------------------------------------
Pass '412' as the parameter, and the desired S-Curve strength [0,8] as the value.

A value of 0 represents no S-Curving (trapezoidal profiling).

To set the S-Curve strength in LabVIEW, the following LV snippet can be used.

.. tip:: Drag and drop the bottom image into your LabVIEW Block Diagram.

.. image:: img/lv-scurve.png

Stator Current Limit Threshold Configs
-----------------------------------------
The trigger threshold current and time are not honored in 20.0.0 firmware.
Stator current limit will trigger when the measured current exceeds the limit (within 1ms).


CANCoder not a remote sensor source
-----------------------------------------
CANCoder is not available as a remote sensor source for Talon FX/SRX and Victor SPX.  This will be addressed in a future update.

.. tip:: This was added in Phoenix v5.17.6.  Motor Controller must be updated to 20.1 or newer.


Remote Sensors Not Working with Talon FX
-----------------------------------------
The remote sensor feature does not work with Talon FX.

.. tip:: This is fixed in firmware version 20.1


LabVIEW 2020 Deploys failing
-----------------------------------------
During our system level validation, we observed a circumstance where LabVIEW permanent deploys would fail ("Connection disconnected by peer").
We are currently investigating this, but we will tentatively report the following suggestions until we complete our assessment.

- When deploying LabVIEW, we recommend disconnecting Phoenix Tuner to ensure it doesn't influence LabVIEW's deploy process.
- If deploys are consistently failing, the running LabVIEW application can be cleared via SSH with ``/usr/local/frc/bin/frcKillRobot.sh -t -r`` or press the UnDeploy LabVIEW/Diag Server button in Tuner - Robot Controller Install.  This should bring the roboRIO into an empty state whereby deploy can be re-attempted.
- Alternatively roboRIO could also be reset using DriverStation "Reboot roboRIO" button.  This is effective if roboRIO is running a temporary deployed LV application or temporary diagnostic server.

.. tip:: This has been resolved in Phoenix v5.17.4.

TalonFX Current Reporting Status Frame Not Available
----------------------------------------------------
The Status Frame that TalonFX uses when reporting its supply and stator current is not available under the StatusFrame or StatusFrameEnhanced enum.
The enum will be modified to include this frame in a future update. 
Currently, the following can be done to modify the Current Measurement Status Frame period:

.. code-block:: java

    _fx.setStatusFramePeriod(0x1240, periodMs); //0x1240 is used to identify the Current Status Frame

.. tip:: This has been resolved in Phoenix v5.17.6.

Talon FX Thermal Limits Low when using PWM Out-of-the-Box
----------------------------------------------------------------
Talon FX's ship firmware has lower thermal limits that current firmware.
If using the Talon FX with PWM control, users may still want to update firmware over CAN to take advantage of the higher thermal limits.