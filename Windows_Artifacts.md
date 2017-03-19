## REGISTRIES

1. **NTUSER.dat:**  Location:Win2003-: Document and Settings\, Vista+: Users\
   * **OpenSaveMRU:** Tracks files opened or saved within a Windows shell dialog box
     * Location: XP NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSaveMRU
                 Win7 NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePIDlMRU
   * **LastVisited/MRU:** Tracks executables used by app to open documents in OpenSaveMRU key
     * Each list could have a diff method for identifying order
     * Location: XP NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedMRU  
                 Win7 NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedPidlMRU
   * **Recent Files:** tracks files or folders within the "Recent" under the start menu
     Location: NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs
   * **Office Recent Files:** Office specific recent files
    Location: NTUSER.DAT\Software\Microsoft\Office\VERSION
      14.0 = Office 2010, 12.0 = Office 2007, 11.0 = Office 2003, 10.0 = Office XP
   * **RunMRU:** Tracks app run under start->programs choice
    Location: NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU
   * **UserAssist:** track user interaction within Explorer shell for clicks
    Location: NTUSER.DAT\Software\Microsoft\Windows\Currentversion\Explorer\UserAssist\{GUID}\Count
    including start-programs but not start-run and typing app name
    Contains 2+ keys of GUIDs, 64-bit timestamp (last time run) and a occurance count
	UEME_RUNPATH indicates an executable file was accessed
	UEME_RUNPIDL is a pointer to an ItemIdList structure, i.e. a folder or shortcut
	UEME_RUNCPL referring to Control Panel applets being clicked
   * **MUICache:** (XP, 2003), Executables w/o dates based on shell interactions
   * **Shellbags:** (XP, 2003 only): Tracks Explorer viewing preferences
    Can contain GUID to folder MRU, control panel, MFT reference number, external storage, zipped archives, explorer ftp
    Location: XP NTUSER.DAT\Software\Microsoft\Windows\Shell\Bags
              XP NTUSER.DAT\Software\Microsoft\Windows\Shell\BagMRU
              XP NTUSER.DAT\Software\Microsoft\Windows\ShellNoRoam\Bags
              XP NTUSER.DAT\Software\Microsoft\Windows\ShellNoRoam\BagMRU
              Win7 USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\Bags
              Win7 USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\BagMRU
              Win7 NTUSER.DAT\Software\Microsoft\Windows\Shell\BagMRU
              Win7 NTUSER.DAT\Software\Microsoft\Windows\Shell\Bags
   * **XPSearch:** NTUSER.DAT\Software\Microsoft\SearchAssistant\ACMru\####
   * **Win7Search (WordWheelQuery):** NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery
   * **TypedPath:** Typed in Explorer or right of Windows icon
    Location: ntuser.dat\Software\Microsoft\Windows\CurrentVersion\Explorer\TypedPaths
   * **TypedURL:** IE url's entered
    Location: NTUSER.DAT\Software\Microsoft\Internet Explorer\TypedURLs
   * **MountPoints2:** Find users that accessed a USB device
    Last write time of key is the last time the USB device was attached
    Location: NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\MountPoints2
   * **Runkey:** starts at user login. Too many locations to list.
        RunOnce: Deleted after running unless prepended with "!"
   * **TrustRecords:** User clicked enable editing in Office. Not indicator of Enable Macros.
    Location: HKCU\Software\Microsoft\Office\15\Word\Security\Trusted Documents\TrustRecords

2. **SECURITY**
   * Location: \windows\system32\config\SAM
   * Audit policy query
  
3. **SAM**
   * Location: \windows\system32\config\SAM
   * Local Users and Groups and their security identifiers
   * Users Key: SAM\Domains\Account\Users
  
4. **SYSTEM**
   * Services
   * Keys of interest
   * Prefetch is disabled/enabled in HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SessionManager\
     *  Memory Management\PrefetchParameters
   * Contains: ClearPagefileAtShutdown
     *	Existing Page Files
     *	PagingFiles
   * NtfsDisableLastAccessUpdate
   * NtfsDisable8dot3NameCreation
   * AppCompatCache: App compatibility db
     * Location: XP           SYSTEM\CurrentControlSet\Control\SessionManager\AppCompatibility
                 Win7,Win2003 SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache
     * Provides: last modify date and file path
     * For Win7 and later, this moved out of registry to Amcache and RecentFileCache.bcf
   * Legacy Registry Keys: First time service executed, DLL/driver path
   * USB: Devices recorded under ControlSet00#\Enum\USBStor/USB
     Mounts of them under MountedDevices and Control\DeviceClasses

5. **SOFTWARE**
   * Vista/Win7 Network History: Tracks networks, last access time, SSID, domain name, gateway MAC
   *  Location: SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signatures\Unmanaged
                SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signatures\Managed
                SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Nla\Cache
   * ProfileList both local and domain
   * Networking Config
   * Run key for persistence by administrator - boottime
   * Winlogin Notify key
   * Persistence
     * Image File Execution Options / StickyKeys  (runs app at other app exec)
     * appinit_DLLs (inject dll's into path)
     * Shell Extensions
     * Browser Helper Object (BHO)
     * Scheduled Tasks (can exec at login) schtasks & at
     * Autostart: InProcServer (Software, NTUser, USRClass) 
   * SysInternals keys eg. Software\SysInternals\Strings = EulaAccepted
     * Time relates to when app was first run
   * Disable UserAssist: 
     * Location: XP HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist
                 Vista HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced\Start_TrackProgs
   
6. **USRCLASS.DAT**
   * Location: Win2003- : Local Settings\Application Data\Microsoft\Windows\
               Vista+   : AppData\Local\Microsoft\Windows\99999
   * MUICache : (Vista+) Executables w/o dates based on shell interactions
   * Shellbags: (Vista+)
   * Autostart: InProcServer (Software, NTUser, USRClass)

7. **Amcache.hve:** Win8 replacement of RecentFileCache.bcf
   * Location: \Windows\AppCompat\Programs\Amcache.hve
   * Provides: volume guid, first run, file path, file size, SHA1
   * Program subkey contains MSI installed files

## NON-REGISTRY ARTIFACTS

8. **Jumplists in Win7+**
   * Path: %AppData%\MicrosoftAppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations
   * Provides: First time of execution, last time of execution

9. **RecentFileCache.bcf:** Win compatibility DB
   * Location: C:\Windows\AppCompat\Programs\

10. **Prefetch:** Increases performance by pre-loading code pages of run apps
    * Location: Win7/XP C:\Windows\Prefetch
    * disabled on server builds 
    * Executable, run count, size of pf, files/dirs referenced, volume
    * pf creation is first execution
    * last modify time is last time it was executed
    * Examine files/dir mapped by this and for files in close time prox
  
11. **MFT**
    * Full filename
    * Parent directory
    * File size, Creation Date, Mod Date, MFT Change Date, Access Date
    * Change times cannot be edited with a Windows API
    * $File_name timestamps are based on movement in b-tree
    * $Standard_Information timestamps are for MACE. Easily timestomped
    * $I30 timestamps are FN not SI timestamps

12. **USNJrnl**
    * Records file/folder changes
    * Time of Change, reason, file/dir name, MFT record number, 
  
13. **Shortcut LNK files:** Automatically created links
    * Location: XP C:\Documents and Settings\<username>\Recent\
                Win7 C:\Users\<user>\AppData\Roaming\Microsoft\Windows\Recent\
                Win7 C:\Users\<user>\AppData\Roaming\Microsoft\Office\Recent\
    * First and last time of opening (creation and last modified date)
    * LNKTarget File (Internal LNK File Information) Data:
      * Modified, Access, and Creation times of the target file
      * Volume Information (Name, Type, Serial Number), Name of System
      * Network Share information, Original Location
    
14. **Applets:** eg. regedit, wordpad, ms paint
    * regedit nas lastkey value
    * wordpad has recent file list
  
15. **SRUM (System Resource Utilization Manager database)**
    * Location: \Windows\sru
    * Network and length of connection, bytes written to HDD, applications executed with SID and runtimes

16. **IExplore index.dat:** IE activity.  Local and remote file activity via network shares
    * Does not limit to actiity run in Internet Explorer 
    * Location: XP %userprofile%\Local Settings\History\History.IE5
                Win7 %userprofile%\AppData\Local\Microsoft\Windows\History\History.IE5
                Win7 %userprofile%\AppData\Local\Microsoft\Windows\History\Low\History.IE5