# Tutoriel-ILCSoft

## Table des matières
-[Exercice 1](https://github.com/EmilioBrs/Tutoriel-ILCSoft/edit/main/README.md#exercice-1)

-[Exercice 2](https://github.com/EmilioBrs/Tutoriel-ILCSoft/edit/main/README.md#exercice-2)

-[Marlin](https://github.com/EmilioBrs/Tutoriel-ILCSoft/edit/main/README.md#marlin)

-[Create a ROOT ntuple from LCIO](https://github.com/EmilioBrs/Tutoriel-ILCSoft/edit/main/README.md#create-a-ROOT-ntuple-from-LCIO)

-[Build the MyMarlin example package](https://github.com/EmilioBrs/Tutoriel-ILCSoft/edit/main/README.md#build-the-mymarlin-example-package)
```
git clone https://github.com/iLCSoft/ILDConfig.git -b v02-02-02
```
```
cd ILDConfig/StandardConfig/production/
```
```
. /cvmfs/ilc.desy.de/sw/x86_64_gcc82_centos7/v02-02-02/init_ilcsoft.sh
```
```
ddsim -h
Marlin -h
dumpevent -h
g++ -v
```
```
ddsim --inputFiles Examples/bbudsc_3evt/bbudsc_3evt.stdhep \
--outputFile=./bbudsc_3evt_SIM.slcio \
--compactFile $lcgeo_DIR/ILD/compact/ILD_l5_v02/ILD_l5_v02.xml \
--steeringFile=./ddsim_steer.py > ddsim.out 2>&1 &
```
## Exercice 1
```
gedit ddsim_steer.py &
```

## Exercice 2
```
anajob bbudsc_3evt_SIM.slcio
```
```
dumpevent -h
```
```
export LCIO_READ_COL_NAMES="HCalBarrelRPCHits HcalBarrelRegCollection"
```
```
dumpevent bbudsc_3evt_SIM.slcio 1 | less
```
## Marlin
```
Marlin MarlinStdReco.xml \
--constant.lcgeo_DIR=$lcgeo_DIR \
--constant.DetectorModel=ILD_l5_o1_v02 \
--constant.OutputBaseName=bbudsc_3evt \
--global.LCIOInputFiles=bbudsc_3evt_SIM.slcio \
> marlin.out 2>&1 &
```
## Create a ROOT ntuple from LCIO
```
Marlin --global.LCIOInputFiles=bbudsc_3evt_REC.slcio \
MarlinStdRecoLCTuple.xml
```
```
cd RootMacros
```
```
root -l
```
après root [0] :
```
.x ./draw_simhits.C("../StandardReco_LCTuple.root")
```
## Reading an slcio file via ROOT
```
root -l read_slcio.C
```

