# WFMConverter
Converts .wfm files to .txt files

You need the boost libraries installed before it will compile. http://www.boost.org

Then the way you run it is:

$> ./convert   /InputData/File/Location/   someCommonNameString   desiredOutputName

The someCommonNameString is for combining similar data runs, i.e.

runA_1.wfm
runA_2.wfm
runA_3.wfm

You would put runA_ as the someCommonNameString and then the output would be desiredOutputName.fff


The output format is:

channel1waveformEvt1 channel2waveformEvt1 … channelNwaveformEvt1
channel1waveformEvt2 channel2waveformEvt2 … channelNwaveformEvt2
.
.
.
channel1waveformEvtN channel2waveformEvtN … channelNwaveformEvtN



For example, If you took data with two channels, and each waveform was 5 samples, you would see:

1 1 1 1 1 2 2 2 2 2 

where the first 5 samples are from channel 1, and the second 5 samples are channel from 2.

There is no timing information in this output file.  You need to consult the header (.hea) file for the # of samples and the corresponding time / point, or record the scope settings for each data run.  Each point listed is a 
voltage reading (in mV or V, depends on setting) for the specific time slice in the waveform.  Look in the convert.sh script to enable .hea info.

With this particular scope, you will likely be running 2 channels simultaneously, which can afford you a maximum of 20 GS/s.  If you're set to 10 ns / division, with 10 divisions, that gives you a window of 100 ns and 2000 
samples.  (add 32 to this calculation, no matter the # of samples you get.  If you calculated 1000 samples, there will be 1032 points / channel….2000 samples, 2032 points / channel.)

Therefore, at 20 GS/s and a 100 ns time window, and two channels enabled, you will see 4064 entries on a given line.
