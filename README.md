# DarkPhotonAnalysisV2

For 2022 data nTuple production:

```
#!/bin/bash
RELEASE=CMSSW_12_4_10

source /cvmfs/cms.cern.ch/cmsset_default.sh
scram p CMSSW $RELEASE
cd $RELEASE/src
git clone -b F03 https://github.com/z4027163/darkphoton_run3.git
eval `scram runtime -sh`
scram b -j8
cd ../..
cp $RELEASE/src/darkphoton_run3/DimuonAnalysis/test/template2022_cfg.py scout2022_cfg.py

#or have some input.root
xrdcp root://cms-xrd-global.cern.ch//$1 input.root 

cmsRun scout2022_cfg.py

oname=`echo $1 | sed 's/.*\///'`
#transfer output
mv output.root $oname
xrdcp -f $oname root://submit50.mit.edu//store/user/wangzqe/darkphoton/run3/

```


For 2023 data nTuple production:

```
#!/bin/bash
RELEASE=CMSSW_13_0_13

source /cvmfs/cms.cern.ch/cmsset_default.sh
scram p CMSSW $RELEASE
cd $RELEASE/src
git clone -b F03 https://github.com/z4027163/darkphoton_run3.git
eval `scram runtime -sh`
scram b -j8
cd ../..
cp $RELEASE/src/darkphoton_run3/DimuonAnalysis/test/template2023_cfg.py scout2023_cfg.py

#or have some input.root
xrdcp root://cms-xrd-global.cern.ch//$1 input.root

cmsRun scout2023_cfg.py

oname=`echo $1 | sed 's/.*\///'`
#transfer output
mv output.root $oname
xrdcp -f $oname root://submit50.mit.edu//store/user/wangzqe/darkphoton/run3/

```

