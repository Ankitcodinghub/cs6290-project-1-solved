# cs6290-project-1-solved
**TO GET THIS SOLUTION VISIT:** [CS6290 Project 1 Solved](https://www.ankitcodinghub.com/product/cs-6290-high-performance-computer-architecture-solved/)


---

📩 **If you need this solution or have special requests:** **Email:** ankitcoding@gmail.com  
📱 **WhatsApp:** +1 419 877 7882  
📄 **Get a quote instantly using this form:** [Ask Homework Questions](https://www.ankitcodinghub.com/services/ask-homework-questions/)

*We deliver fast, professional, and affordable academic help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;126105&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;2&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (2 votes)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;CS6290 Project 1 Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (2 votes)    </div>
    </div>
&nbsp;

This project is intended to help you understand branch prediction and performance of outof-order processors. You will again need the “CS6290 Project VM” virtual machine, the same one we used for Project 0. Just like for Project 0, you will put your answers in the red-ish boxes in this Word document, and then submit it in Canvas (the submitted file name should now be PRJ1.docx).

Additional files to upload are specified in each part of this document. Do not archive (zip, rar, or anything else) the files when you submit them – each file should be uploaded separately, with the file name specified in this assignment. You will lose up to 20 points for not following the file submission and naming guidelines, and if any files are missing you will lose all the points for answers that are in any way related to a missing file (yes, this means an automatic zero score if the PRJ1.docx file is missing). Furthermore, if it is not VERY clear which submitted file matches which requested file, we will treat the submission as missing that file. The same is true if you submit multiple files that appear to match the same requested file (e.g. several files with the same name). In short, if there is any ambiguity about which submitted file(s) should be used for grading, the grading will be done as if those ambiguous files were not submitted at all.

Most numerical answers should have at least two decimals of precision. Speedups should be computed to at least 4 decimals of precision, using the number of cycles, not the IPC (the IPC reported by report.pl is rounded to only two decimals). You lose points if you round to fewer decimals than required, or if you truncate digits instead of correctly rounding (e.g. a speedup of 3.141592 rounded to four decimals is 3.1416, not 3.1415).

As explained in the course rules, this is an individual project: no collaboration with other students or anyone else is allowed.

Part 1 [20 points]: Configuration of the Branch Predictor

The hardware of the simulated machine is described in the configuration file. In this project we will be using the cmp4-noc.conf configuration file again, but this time we will modify this file so this is a good time to make a copy so we can restore the original configuration when we need it.

The processors (cores) are specified in the “cpucore” parameter near the beginning of the file. In this case, the file specifies that the machine has 4 identical cores numbered 0 through 3 (the procsPerNode parameter is 4), and that each core is described in section [issueX]. Going to section [issueX], we see that a core has a lot of parameters, among which we see that the clock frequency is set at 1GHz, that this is an out-of-order core (inorder set to false) which fetches, issues, and retires up to 2 instructions per cycle (the “issue” parameter is set to two earlier in the file). The core has a branch predictor described in the [BPredIssueX] section, fetches instructions from a structure called “IL1” described in the [IMemory] section (this is specified by the instrSource parameter, and reads/writes data from a structure called “DL1” described in the [DMemory] section. In this part of this project, we will be modifying the branch predictor, so let’s take a closer look at the [BPRedIssueX] section. It says that the type of the predictor is “Hybrid” (which does not tell us much), and then specifies the parameters for this predictor.

The “Hybrid” predictor is actually a tournament predictor. You now need to look at its source code (which is in BPred.h and BPRed.cpp files in the ~/sesc/src/libcore/ directory) and determine which of the parameters in the configuration file controls which aspect of the predictor. Hint: the “Hybrid” predictor is implemented in the BPHybrid class, so its constructor and predict method will tell you most of what you need to find out.

2048

2

global

2 -bit counters, and has 2048

localSize

8

2048

l2size ), and each entry is a 1

A) The meta-predictor in this hybrid predictor is a table that has entries and each entry is a –bit counter. This meta-predictor decides, based on the PC address (i.e. the address from which we fetched the branch instruction), whether to make the prediction using a simple (no history) array of counters, or to use a (is it local or global?) history predictor. The simpler (non-history) predictor uses of them (this number is specified using a parameter label in the BPredIssueX section of the configuration file). The history-based predictor has bits of history, which are combined with the PC address to index into an array that has entries (this number of entries is specified in the configuration file using parameter label -bit counter.

Part 2 [30 points]: Changing the Branch Predictor

Now we will compare some branch predictors. The LU benchmark we used in Project 0 does not really stress the branch predictor, so we will use the raytrace benchmark:

cd ~/sesc/apps/Splash2/raytrace make

Now it is time to do some simulations:

A) Simulate the execution of this benchmark using the unmodified cmp4-noc configuration (with the “Hybrid” predictor). The following should all be a single command line, which has a space before -ort.out. As before, the dashes in

this command line should be the minus character but a copy-paste might result in something else that looks similar but is not a minus character, so be careful is you are copy-pasting.

~/sesc/sesc.opt -f HyA -c ~/sesc/confs/cmp4-noc.conf ort.out -ert.err raytrace.mipseb -p1 -m128 -a2

Input/reduced.env

Then we will modify the configuration file, so make a copy of it if you did not do this already. Then change the configuration to model an oracle (perfect) direction predictor by changing the “type” of the predictor from “Hybrid” to “Oracle”, then and re-run the simulation (change the -f parameter to -f OrA so the simulation results are written to a different file). Note that overall branch prediction accuracy is not perfect in this case – only the direction predictor is perfect, but the target address predictor is a (non-oracle) BTB! After that, configure the processor to use a simple predict-not-taken predictor (type=”NotTaken”) and run the simulation again (now using -f NTA). Submit the three simulation report files (sesc_raytrace.mipseb.HyA, sesc_raytrace.mipseb.OrA, and sesc_raytrace.mipseb.NTA) in Canvas along with the other files for this project.

B) In the table below, for each simulation fill in the overall accuracy (number under BPred in the output of report.pl), the number of cycles, and the speedup relative to the configuration that uses the Hybrid predictor. BPred Accuracy

C) Now change the processor’s renameDelay parameter (in the issuesX section of the configuration file) from 1 to 8. This makes the processor’s pipeline 7 stages longer.

Repeat the three simulations, submit the simulation report files (sesc_raytrace.mipseb.HyC, sesc_raytrace.mipseb.OrC, and sesc_raytrace.mipseb.NTC) in Canvas along with the other files for this project.

D) In the table below, fill in the number of cycles with each type of predictor from Part A (simulations with the default pipeline depth) and from Part C (when the pipeline is 6 stages deeper), then compute the speedup of shortening the pipeline for each type of predictor, assuming that the clock cycle time stays the same (so the speedup can be computed using the number of cycles instead of execution time).

E) The results in Part E) lead us to conclude that better branch prediction becomes

more

(more or less?) important when the processor’s pipeline depth increases. Explain why:

CPI is equal to 1 + (mispredictions/instruction) * (penalty/misprediction). With that in mind, if we take a look at the equation when the pipeline depth increases so does the penalty for each misprediction. Now if the penalty increases for each misprediction, the percentage of times it will mispredicted has to be low in order to get a CPI, or else if the predictor isn’t accurate, the (mispredictions/instruction) is only going to increase and you multiply that by the (penalty/misprediction), you’re not going to get a good CPI. Now if the predictor is very accurate, then the (misprediction/instruction) section will be smaller as a result will minify the result of (penalty/misprediction), resulting in a better CPI.

41

F) From simulation results you have collected up to this point, there are at least two good ways to estimate how many cycles are wasted when we have a branch misprediction in the processor that has the default pipeline depth, i.e. what the branch misprediction penalty (in cycles) was for simulations in Part A). Enter your best estimate here and then explain how you got it:

As mentioned above the CPI is calculated as CPI = Ideal CPI +

(mispredictions/instruction) * (penalty/misprediction). To get the misprediction penalty we need to solve for (penalty/misprediction) or how many penalties per misprediction. The Ideal CPI in this case would be 0.5 because at the beginning it is mentioned that this simulator fetches, issues, and retires up to 2 instructions per cycle or 2 IPC. The CPI is just the multiplicative inverse of the IPC making it ½ or

0.5. So with that in mind, here’s how I calculated the penalty for the hybrid predictor. With the reporting script, I was able to find that the IPC was 0.84, so the actual CPI was 1/0.84. Now we need to calculate the mispredictions/instruction. For that we need the total predictor accuracy and the percentage of instructions that were jump instructions because those instructions require the predictor. That was calculated by doing (1 – Total Accuracy %) – Jump Instructions %. After getting those values, the (penalty/misprediction) can be calculated using (CPI – Ideal CPI)/(mispredictions/instruction). Using that I got approx. 41.18 which rounded down came to be 41 cycles per misprediction.

Part 3 [50 points]: Which branches tend to be mispredicted?

In this part of the project we again use the cmp4-noc configuration. You should change it back to its original content, i.e. what it had before we modified it for Part 2. We will continue to use the Raytrace benchmark with the same parameters as in Part 2.

Our goal in this part of the project is to determine for each instruction in the program how many times the direction predictor (Hybrid or NotTaken) correctly predicts and how many times it mispredicts that branch. The number of times the static branch instruction was completed can be computed as the sum of two (correct and incorrect predictions) values for that static branch instruction. You should change the simulator’s code to count correct and incorrect predictions for each static branch instruction separately, and to (at the end of the simulation) print out the numbers you need to answer the following questions. The printing out should be in the order in which the numbers are requested below, and your code should not be changing the simulation report in any way. Then you should, of course, run the simulation and get the simulation results with the Hybrid and also with the NT predictor.

1056

473

G) In both simulations, the number of static branch instructions that are completed at least once but fewer than 20 times (i.e. between 1 and 19 completions) is , the number of static branch instructions with 20 to 199 completions is

155

654

, the number of static branch instructions with 200 and 1999 completions is , and the number of static branch instructions with 2000+ completions is

.

H) The accuracy for the direction predictor, computed separately for the four groups of static branch instructions (1-19, 20-199, 200-1999, and 2000+ completions), is a follows:

I) We cannot run the raytrace benchmark with a much larger input because the simulation time would become excessive. But if we did, concisely state what would happen to the overall direction predictor accuracy of the Hybrid predictor and of the NT predictor, and then explain why the predictor accuracy should change in the way you stated.

J) Submit the BPred.h and BPred.cpp files that you have modified to produce the numbers you needed for Part 3 of this project. If you have modified any other source code in the simulator, create an OtherCode.zip file that includes these files and submit it, too. Also submit the output of the simulator for the two runs (as rt.out.Hybrid and rt.out.NT) Note that there is no need to submit the simulation report files (these should be the same as those from Part A).
