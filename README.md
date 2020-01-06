To setup Bfinder
=====

Ref: https://twiki.cern.ch/twiki/bin/viewauth/CMS/HiForestSetup#Setup_for_10_3_X_2018_PbPb_data

Branch for CMSSW_10XX Recommended using 
* `CMSSW_10_3_1` for data (prompt-reco)
* `CMSSW_10_3_3_patch1` for data (re-reco) and MC (official)

```
cmsrel CMSSW_10_3_3_patch1 # replace CMSSW_10_3_2 with the proper release
cd CMSSW_10_3_3_patch1/src
cmsenv
git cms-merge-topic -u CmsHI:forest_CMSSW_9_4_10
git remote add cmshi git@github.com:CmsHI/cmssw.git
cd HeavyIonsAnalysis/JetAnalysis/python/jets
./makeJetSequences.sh
cd ../../../..
scram build -j4
```

To add D/Bfinder to forest:
=====

```
cd $CMSSW_BASE/src
cmsenv
git clone -branch Dfinder_10XX https://github.com/boundino/Bfinder.git --depth 1
source Bfinder/test/DnBfinder_to_Forest_103X.sh
scram b -j4
# Bfinder MC:
mkdir -p bfinder && cp HeavyIonsAnalysis/JetAnalysis/test/runForestAOD_pp_MC_94X_onlyBfinder.py bfinder/runForestAOD_pp_MC_94X_onlyBfinder.py
# Bfinder data:
mkdir -p bfinder && cp HeavyIonsAnalysis/JetAnalysis/test/runForestAOD_pp_DATA_94X_onlyBfinder.py bfinder/runForestAOD_pp_DATA_94X_onlyBfinder.py
cd bfinder/
```

To run:
=====

* MC:
```
cmsRun runForestAOD_pp_MC_94X_onlyBfinder.py
```
* data:
```
cmsRun runForestAOD_pp_DATA_94X_onlyBfinder.py
```
