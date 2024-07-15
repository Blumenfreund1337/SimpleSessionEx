This is a README that explains how to use the short Library that i created

after importing the functions_v7 data you get access to a bunch of functions that make it easier to work with the ONE and brainbox.io API


CREATESESSION()
first you create an Object of the class Session by calling createSession() with the Parameters you want to search for 
im shortly gonna explain every parameter:
Roi (default : Roi = ""): Roi is short for Region of Interest and it takes an Region of the brain by the short name of the AllenAtlas for example "SNr" or "SI" 

pid (default : pid = ""): the Pid is the id of the Probe, normally after my final understanding every EID, which means session ID has many PIDs but every PID has one EID. A PID looks like this: "6a7544a8-d3d4-44a1-a9c6-7f4d460feaac"

POn (default : POn = False): POn is short for PrintOn and it helps to get a better understanding of what data you get, if set on True you will recieve Print in your Terminal, telling you how many Session, Cluster and Spikes where found

sessNmb (default : sessNmb= 0): sessNmb is short for Session Number and is just a Number to choose for the found Sessions, for example if you find 22 Session the function will take the Session debending on the sessNmb. 0 is just the first of these Sessions

EID (default : EID = ""): The EID is the Session ID and looks like PID, a long ID. Every Session has one and it helps finding the exact same session, but if your searching for a specific Probe ID it may not guarante to find the same PID every time. Watch out for that
 
lab (default : lab =""): Its just if you want to filter for a specific Lab, for example "steinmetzlab"
 
nmb (default : nmb =""): Its another filter option you can search for a EID, I dont understand it, it is not unique its a single number I dont know why you should search by that alone.

porj (default : proj =""): stands for Project and its Project name of the session. An example would look like that: 'ibl_neuropixel_brainwide_01' 

starTime (default : starTime = ""): it is the Start Time of the session looking something like this for example: '2022-08-12T16:56:27.875789'

subj (default : subj=""): This is the subject of the session. Its the Name of the little mouse that was given by the lab. A subject Name can look like this 'UCLA049tas'

TaskProt (default : taskProt = ""): stands for Task Protokoll and looks like these '_iblrig_tasks_ephysChoiceWorld6.6.2' 



CLASS SESSION 
The Session Class automatically gets created when using createSession() as input it just needs the session the eid and pid of the session depending on what it is. giving in a pid gets you everything but puting in the eid could result in not having a pid because there are some Sessions that have no PIDs.

The class has 9 Attributes at the moment. It saves:
The whole session itself as the sess attribute

The PID and EID in a attribute each called sessPID and sessEID

cluster, spikes and channel are 3 attributes that get created automatically when there is a PID found and can be called like any attribute. These three are dictionaries so for example you can call "objectname.cluster["channels"]" to get the Array with the clusters.

PrintOn is a simple true false variable. its usage is explained up in createSession()

sessionEIDInfo is a dictionary that has the basic SessionInfo and can look like this: {'id': '8a1cf4ef-06e3-4c72-9bc7-e1baa189841b', 'subject': 'UCLA049', 'start_time': '2022-08-12T16:56:27.875789', 'number': 1, 'lab': 'churchlandlab_ucla', 'projects': ['ibl_neuropixel_brainwide_01'], 'url': 'https://openalyx.internationalbrainlab.org/sessions/8a1cf4ef-06e3-4c72-9bc7-e1baa189841b', 'task_protocol': '_iblrig_tasks_ephysChoiceWorld6.6.2'}


trials is a dictionary with many useful data. It works the same here, the keys are: ['stimOff_times', 'goCueTrigger_times', 'goCue_times', 'response_times', 'choice', 'stimOn_times', 'contrastLeft', 'contrastRight', 'probabilityLeft', 'feedback_times', 'feedbackType', 'rewardVolume', 'firstMovement_times', 'intervals']


getClusterAndSpikesOfSess()
This method is not meant to be used normaly. It is just there to run when a session object is created. It automaticly creates cluster, spikes and channel for the attribuites.


getEIDinfo()
it also is meant to just fill in the sessEIDInfo attribute by looking at the PID info


getMainInfo()
it returns [EID, PID, subject, lab] 


getLineGraph()
its usage is to create a Graph of the spikes to show the firing rates of them 
events1 is a parameter that takes in the event that is supposed to be checked for example 'stimOn_times'

Roi is the Region of Interest and is required so that the function can search in the clusters of the sesion for a fitting cluster

figsize1 (default : figsize1 =(7,7)): is there to genererate the size of the plot. it has a fitting default but can be adjusted 

intervall1 (default : intervall1 = [0.2, 0.5]): is for the intervall of the graph that is getting plottet. Just give in a list for example: "[0.5, 2]

bin_size1 (default : bin_size1= 0.025): the size of the bins

smoothing1 (default : smoothing1=0.025): is the the visual smoothing of the graphh

as_rate1 (default : as_rate1 = True): Whether to use spike counts or rates in the plot

include_raster1 (default : include_raster1=False): Whether to put a raster below the PETH of individual spike trains

n_raster1 (default : n_raster1= None) If include_raster is True, the number of rasters to include. If None will default to plotting rasters around all provided events.

error_bars1 (default : error_bars1='std'): It can be "std","sem" or "none". Defines which type of error bars to plot. Options are: – ‘std’ for 1 standard deviation – ‘sem’ for standard error of the mean – ‘none’ for only plotting the mean value 

pethline_kwargs1 (default : pethline_kwargs1 = {'color': 'blue', 'lw': 2}): Dict containing line properties to define PETH plot line. Default is a blue line with weight of 2. Needs to have color. See matplotlib plot documentation for more options. 

errbar_kwargs1 (default : errbar_kwargs1 = {'color': 'blue', 'alpha': 0.5}): Dict containing fill-between properties to define PETH error bars. Default is a blue fill with 50 percent opacity.. Needs to have color. See matplotlib fill_between documentation for more options. 

eventline_kwargs1 (default : eventline_kwargs1={'color': 'black', 'alpha': 0.5}):  Dict containing fill-between properties to define line at event. Default is a black line with 50 percent opacity.. Needs to have color. See matplotlib vlines documentation for more options.

raster_kwargs1 (default : raster_kwargs1={'color': 'black', 'lw': 0.5}): Dict containing properties defining lines in the raster plot. Default is black lines with line width of 0.5. See matplotlib vlines for more options.

xlab/ylab (default : xlab =""/ylab = ""): the names for the x and y axes of the graph

pidnmb (default : pidnmb = 1): The number of the PID choosen for the plot

getAcronymInfo()
returns an dictonary that is sorted by the cluster brain region and has the number of the specific cluster still saved. for example if the cluster number 207, 231 and 244 are "SNr" cluster the dictionary looks like this: {"SNr" : [207,231,244]} That way you can still find the exact cluster when going over the normal cluster list. 

getSpecificTrials()
reutrns a list with trial data in this order: ['goCueTrigger_times', 'feedback_times', 'stimOff_times, 'stimOn_times', 'firstMovement_times', 'rewardVolume']


getStimOnOff()
this method returns a list that has the Stim On and Off times in one list sorted with: ['stimOn', 'stimOff', 'stimOn', 'stimOff']

getTrialStart()
returns a list that contains all trial start times by looking at the feedback times and depending if the subject got a treat adds 1 second or 2

getTommyStuff()
returns a list that cpntains the following in that order [goCueTRigger, feebbackTimes, rewardVolumme, stimOn/Off times, firstMovment, trialstarts]


getClusterPos()
a function that returns the cluster position of an session as a list with an (X,Y,Z) tuple for each entry
just input the cluster dictionary as a parameter 

pidsofSessions()
a simple function that just returns a bunch of IDs of the Probes. you can give in a Brain region as a parameter. That way you can get all the Probes where this brain section is included