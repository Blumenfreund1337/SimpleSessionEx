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


t_before (default : t_before1 = 0.2): just the time before point zero how much of the x axes should be shown 

t_after1 (default : t_after1 = 0.5): The same as 
 bin_size1= 0.025, smoothing1=0.025, as_rate1 = True, include_raster1=False, 
                            n_raster1= None, error_bars1='std', pethline_kwargs1 = {'color': 'blue', 'lw': 2}, errbar_kwargs1 = {'color': 'blue', 'alpha': 0.5}, 
                            eventline_kwargs1={'color': 'black', 'alpha': 0.5}, raster_kwargs1={'color': 'black', 'lw': 0.5}, xlab ="", ylab = "", pidnmb = 1):