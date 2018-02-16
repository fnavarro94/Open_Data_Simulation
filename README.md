# Open_Data_Simulation
Example on how to run a simulation with your own particle card

## Set up

 Create a CMSSW environment
 '''
 cmsrel CMSSW_5_3_32
 cd CMSSW_5_3_32/src/
 cmsenv
'''
Copy repository
'''
 git clone git@github.com:fnavarro94/Open_Data_Simulation.git
'''
## Running simulation

To perform a generation level simulation:
'''
 cmsRun hlt_cfg.py
'''
To perform a reco level simulation (this uses the output of the gen level simulation as imput):
'''
cmsRun reco_cfg.py
'''
## Configuration

You can change the number of events to be simulated by editing the cfg.py files at:
 > 
 
## About the code:

the gen and reco configuration files where created with the folowing commands respectively:
'''
 cmsDriver.py Pythia_H0_pyupda_7TeV_cfi.py --step=GEN,SIM,DIGI,L1,DIGI2RAW,HLT:2011 --datatier GEN-SIM --conditions=START53_LV6A1::All --fileout=simu_test.root --eventcontent RAWSIM --python_filename hlt_cfg.py --number=10 --mc --no_exec

 cmsDriver.py --filein file:simu_test.root --fileout file:reco_test.root --mc --eventcontent AODSIM --conditions START53_LV6::All --step RAW2DIGI,L1Reco,RECO --python_filename reco_cfg.py --no_exec -n 10 --datatier AODSIM
'''
this needs to be run inside a CMSSW environment.

In order to use your own particle card replace the particle card file name on line 113 of hlt_cfg.py with your own.
E.g:

replace 
'''
PYUPDAParameters = cms.vstring("PYUPDAFILE = \'Configuration/Generator/data/Pythia_H0_pyupda.in
'''
with    
'''
PYUPDAParameters = cms.vstring("PYUPDAFILE = \'my_pyupda.in\'")
'''
