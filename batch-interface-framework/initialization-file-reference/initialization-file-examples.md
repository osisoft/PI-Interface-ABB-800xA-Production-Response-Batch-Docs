---
uid: BIF_InitializationFileExamples
---

# Initialization file examples

## Multiple EVT Sources
```
[SOURCE TEMPLATE] 

Source[1].evtdir=c:\test\evt 
Source[2].evtdir=\\deltav9\\journals\evt 

[GENERAL] 

Excludestates=COMPLETE, ABORTING Equipment = abs:[Unit]\[PhaseModule]\Misc 

[TAG TEMPLATE] 

// [Basic Tag template, triggered on Event=Report, aliases are created as tag name] 

Tag[1].Name = [Unit]_[PhaseModule]_Report 
Tag[1].Value = [Pval] 
Tag[1].Type = Float // [Tag template with custom aliases, triggered on Event=Owner Change] 
Tag[2].Name = [Unit]_[PhaseModule]_Owner Change 
Tag[2].Value = [time]_[Descript] 
Tag[2].Type = String 
Tag[2].unitalias = [PhaseModule] Owner Change Me 
Tag[2].phasealias = Owner Change Me 

// [Tag template with custom aliases, triggered on set of events defined as triggers] 

// [Note: Unitalias and Phasealias are NOT going to be created since there are no Unit or Phase Module 

// defined in the tag name] 

Tag[3].Name = Generic Tag 
Tag[3].Value = [time]_[Event]_[BatchID]_[pval] 
Tag[3].Type=String 
Tag[3].trigger = Report 
Tag[3].trigger = Owner Change 
Tag[3].trigger = Operator Prompt 
Tag[3].unitalias = [phasemodule] abcd 
Tag[3].phasealias = testing [PROPERTY TEMPLATE] Property[1].Value = [Time] State Change [Descript] [pval]
```
## DeltaV German EVT Source
```
[SOURCE TEMPLATE] 

source[1].evtdir = D:\TEST\evt german\evt 

[GENERAL] 

ExcludeStates = NONE 

[TAG TEMPLATE] 
tag[1].Name = German Report 
tag[1].Value = [Descript]:[event][pVal] 
tag[1].Type = string 
tag[2].Name = German Bericht 
tag[2].Value = [Descript]:[event][pVal] 
tag[2].Type = string 
tag[3].Name = German Bericht float 
tag[3].Value = [pVal] 
tag[3].Type = float 

[PROPERTY TEMPLATE] 

Property[1].Value = [Time] Bericht [Unit] [phasemodule] [descript]-[Pval] 
Property[2].Value = [Time] report [Unit] [phasemodule] [descript]-[Pval]

[TRANSLATIONS] 

// [S88 Levels] 
translate: "Grundrezept" = "Procedure" 
translate: "Teilrezept" = "Unit Procedure" 
translate: "Grundoperation" = "Operation" 
translate: "Grundfunktion" = "Phase" 

// [Batch Header info] 

translate: "Rezeptkopf" = "Recipe Header" 
translate: "Produktcode" = "Product Code" 
translate: "Formelkopf" = "Formula Header" 
translate: "Formelname" = "Formula Name" 

// [Arbitrations] 

translate: "Rezeptzuteilung" = "Recipe Arbitration" 
translate: "Betriebsmittel belegt durch Rezept" = "Resource Acquired by recipe" 
translate: "Betriebsmittel freigegeben durch Rezept" = "Resource Released by recipe" 
translate: "Teilanlage" = "Unit" 

// [Recipe Logic, Comment needed only if there is an extra column in DeltaV, so event can be converted to 
// Comment event] 

translate: "Zustands\E4\nderung" = "State Change" 
translate: "Kommentar" = "Comment" 
translate: "Systemmeldung" = "System Message" 
translate: "CHARGEN-Anfang" = "Beginning Of BATCH" 
translate: "CHARGEN-Ende" = "End Of BATCH" 
translate: "Teilrezept gestartet" = "Unit Procedure Started" 
translate: "Teilrezept beendet" = "Unit Procedure Finished" 
translate: "Grundoperation gestartet" = "Operation Started" 
translate: "Grundoperation beendet" = "Operation Finished" 

// [Phase States] 

translate: "L\C4\UFT" = "RUNNING" 
translate: "BEENDET" = "COMPLETE" 
translate: "ENTFERNT" = "REMOVED" 
translate: "GESTOPPT" = STOPPED" translate: "ABGEBROCHEN" = "ABORTED" 

// [Additional Events to translate] 

translate: "Bericht" = "Report" 
translate: "Schrittaktivit\E4\t" = "Step Activity"
```
## DeltaV SQL
```
[SOURCE TEMPLATE] 

source[1].sqlserver = deltav10 source[1].sqldatabase = DVHisDB 
source[2].sqlserver = deltav102 [GENERAL] ExcludeStates = NONE 

[TAG TEMPLATE] 

Tag[1].Name = [Unit] [Phasemodule] Report 
Tag[1].Value = [Descript] 
Tag[1].Type = string Tag[1].unitalias = [phasemodule] Report 
Tag[1].phasealias = Report 
Tag[2].Name = [Unit] [phasemodule] Tester 
Tag[2].Value = [ atched] [Descript]=[event] 
Tag[2].Type = string 
Tag[2].Trigger = Owner Change 
Tag[2].Trigger = Report 
Tag[2].unitalias = [phasemodule] tester alias 
Tag[2].phasealias = tester alias
```
## DeltaV SQL, OPCAE
```
[SOURCE TEMPLATE] 

source[1].opcnode = deltav101 
source[1].opcserver = DeltaV.OPCEventServer.1 source[1].sqlserver = deltav10 
source[1].sqldatabase = DVHisDB [GENERAL] Equipment=Areas\Abs[Area]\ProcessCells\sss_[ProcessCell]\sdf:[Unit]\Phases\[Phasemodule]_testing Product = [Product],Undefined SkipUnits = NULL*, D50* SkipPhases = Clean*, Load* ExcludeStates = IDLE, ABOR*G, STOP*G [TAG TEMPLATE] 

// [DeltaV Tag Templates] 

Tag[1].Name = [Unit] Report Tag[1].Value = [Descript] | [Pval] | [EU] 
Tag[1].Trigger = [Event,value=”Report”] Tag[1].Type = string 
Tag[1].unitalias = NONE Tag[1].unitalias = NONE 

// Multiple events triggering same template 

Tag[2].Name = [Unit] [phasemodule] Tester 
Tag[2].Value = [ atched] [Descript]_[event] 
Tag[2].Type = string 
Tag[2].Trigger = Owner Change 
Tag[2].Trigger = Report 
Tag[2].unitalias = [phasemodule] tester alias 
Tag[2].phasealias = tester alias
```
