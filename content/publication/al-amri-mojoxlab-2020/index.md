---
title: MoJoXlab
authors:
- Riasat Islam
- Mohammad Al-Amri
date: '2020-05-01'
publishDate: '2024-09-23T17:11:47.368539Z'
publication_types:
- article-journal
hugoblox:
  ids:
    doi: 10.21954/ou.rd.c.4815567
abstract: 'MoJoXlab is a MATLAB based custom motion capture analysis software toolkit
  whose aim is to produce freely available motion capture analysis software to be
  used by anyone interested in generating lower limb joint kinematics waveforms using
  any suitable wearable inertial measurement units (IMUs).It can generate joint angles
  of Ankle, Hip and Knee joints in Sagittal, Frontal and Transverse (not available
  for Ankle joint) planes for different functional tasks such as walking, squatting,
  and jumping. The joint kinematics for MoJoXlab is based on Joint Coordinate System
  (JCS) as proposed by Grood and Suntay. MoJoXlab takes sensor orientation data in
  quaternions as input and outputs joint angles in degrees. The algorithm considers
  a static calibration step, where sensor data is captured for calibration purposes
  while the participant maintains a standing pose. This calibration step is then used
  to calculate the joint angles for the dynamic phase of the motion.Data StructureCurrently,
  MoJoXlab is designed to be used on a 7 sensor based setup, with sensors placed in
  the Pelvis, both thighs, both shanks and both feet. Input files should be in quaternions
  for 7 sensors with 28 columns of data in the following order, where each sensor
  consists of 4 columns of quaternion orientations:Pelvis [qa, qb, qc, qd],Right Thigh
  [qa, qb, qc, qd], Right Shank [qa, qb, qc, qd],Right Foot [qa, qb, qc, qd], Left
  Thigh [qa, qb, qc, qd], Left Shank [qa, qb, qc, qd], Left Foot [qa, qb, qc, qd].Output
  files will contain joint angles with 16 columns of data in the following order:Ankle
  Left Sagittal,Ankle Left Frontal,Ankle Right Sagittal, Ankle Right Frontal, Hip
  Left Sagittal,Hip Left Frontal, Hip Left Transverse, Hip Right Sagittal, Hip Right
  Frontal, Hip Right Transverse, Knee Left Sagittal, Knee Left Frontal, Knee Left
  Transverse, Knee Right Sagittal, Knee Right Frontal, Knee Right Transverse. The
  software workflow: -Get Static Calibration Data:Use this button to select the static
  calibration data file. A dialog box will open to allow you to select the calibration
  data file. Be careful as sometimes the dialog box opens behind the app and becomes
  difficult to see. After you have selected the calibration data file. The filepath
  and filename is shown on the adjacent text field. [sample data is provided with
  the main zip folder with filename: sample_StaticCalibrationDataFile.csv]Get Activity
  Data:Use this button to select the dynamic activity file for example, walking, jumping
  or squatting activity data file. A dialog box will open to allow you to select the
  calibration data file. Be careful as sometimes the dialog box opens behind the app
  and becomes difficult to see. After you have selected the calibration data file.
  The filepath and filename is shown on the adjacent text field. [sample data is provided
  with the same zip folder with filename: sample_ActivityDataFile.csv]Sampling Frequency:Use
  this field to input the sampling frequency of the activity data in Hertz (Hz). [use
  60 Hz for sample data]Calculate Joint Angles:Use this button to calculate the joint
  angles. A dialog box will open that will allow you to select the output folder.
  Be careful as sometimes the dialog box opens behind the app and becomes difficult
  to see. The output data file will be saved in this folder. The filename is automatically
  generated and will be shown on the adjacent text field.Joint Angle Waveforms:The
  plotting area shows the joing angles calculated in degrees, for either Ankle, Hip
  or Knee joints, showing left or right side, for either sagittal, frontal or transverse
  planes.MoJoXlab software collection includes the following files:MoJoXlab setup
  file for WindowsMoJoXlab setup file for macOS The zip files consists of:Setup file  README.txt  sample_StaticCalibrationDataFile.csv  sample_ActivityDataFile.csv  sample_OutputFile.csvReference:Islam
  R, Bennasar M, Nicholas K, Button K, Holland S, Mulholland P, Price B, Al-Amri MNon-proprietary
  movement analysis software using wearable inertial measurement units on both healthy
  participants and those with anterior cruciate ligament reconstruction across a range
  of complex tasks: validation studyJMIR Preprints. 17/01/2020:17872DOI: 10.2196/preprints.17872URL:
  https://preprints.jmir.org/preprint/17872'
links:
- name: URL
  url: https://ordo.open.ac.uk/collections/MoJoXlab/4815567
---
