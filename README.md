# ROCAnalyzer
Use the ROC AUC to determine which preselection cuts to add.

# Steps
1. Make histogram root files using the t-channel coffea framework.
2. Submit jobs to condor for backgrounds. Can also do that for signals or run batchRun.py locally for signals using the command below while being in the `t-channel_Analysis` directory:
    `python batchRun.py`
   if signals files are produced locally, move signal files to the output folder mentioned in the next step.
3. hadd all the condor root files using the command below: 
    `python hadder.py -d [sample labels] -H [output folder name] -p [input folder name] -y [year]`
    e.g.
    `python hadder.py -d 2018_QCD,2018_WJets,2018_ZJets,2018_TT -H preStudy_moreAngV_Run2_hadded -p preStudy_moreAngVars_Run2/output-files -y 2018`
4. Modify the `cutsImportant` list variable in `plotStack.py` if necessary. Then run
    `python plotStack.py -d [input folder name]`
    e.g.
    `python plotStack.py -d preStudy_moreAngV_Run2`
5. Move the `allRocValues.pkl` and `yieldValues.pkl` from the input folder in the previous step to a folder that is accessible by `ROCAnalyzer`.
   For now, that folder is `tchannel/coffea_updates/preselectionStudy/[input folder name]`. 
   e.g. `tchannel/coffea_updates/preselectionStudy/preStudy_moreAngV_Run2`
6. Open the `ROCAnalyzer` jupyter notebook, add the following line and run
    `performStudy([input folder name],"_qual_trg")`
    e.g.
    `performStudy("preStudy_moreAngV_Run2","_qual_trg_st")`
    * the second argument in the function above is not necessary for now.
