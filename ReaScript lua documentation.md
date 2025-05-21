# REAPER API Lua Functions

## AddMediaItemToTrack
```
MediaItem reaper.AddMediaItemToTrack(MediaTrack tr)
```

creates a new media item.
## AddProjectMarker
```
integer reaper.AddProjectMarker(ReaProject proj, boolean isrgn, number pos, number rgnend, string name, integer wantidx)
```

Returns the index of the created marker/region, or -1 on failure. Supply wantidx>=0 if you want a particular index number, but you'll get a different index number a region and wantidx is already in use.
## AddProjectMarker2
```
integer reaper.AddProjectMarker2(ReaProject proj, boolean isrgn, number pos, number rgnend, string name, integer wantidx, integer color)
```

Returns the index of the created marker/region, or -1 on failure. Supply wantidx>=0 if you want a particular index number, but you'll get a different index number a region and wantidx is already in use. color should be 0 (default color), or ColorToNative(r,g,b)|0x1000000
## AddRemoveReaScript
```
integer reaper.AddRemoveReaScript(boolean add, integer sectionID, string scriptfn, boolean commit)
```

Add a ReaScript (return the new command ID, or 0 if failed) or remove a ReaScript (return >0 on success). Use commit==true when adding/removing a single script. When bulk adding/removing n scripts, you can optimize the n-1 first calls with commit==false and commit==true for the last call.
## AddTakeToMediaItem
```
MediaItem_Take reaper.AddTakeToMediaItem(MediaItem item)
```

creates a new take in an item
## AddTempoTimeSigMarker
```
boolean reaper.AddTempoTimeSigMarker(ReaProject proj, number timepos, number bpm, integer timesig_num, integer timesig_denom, boolean lineartempochange)
```

Deprecated. Use SetTempoTimeSigMarker with ptidx=-1.
## adjustZoom
```
reaper.adjustZoom(number amt, integer forceset, boolean doupd, integer centermode)
```

forceset=0,doupd=true,centermode=-1 for default
## AnyTrackSolo
```
boolean reaper.AnyTrackSolo(ReaProject proj)
```

No description available.
## APIExists
```
boolean reaper.APIExists(string function_name)
```

Returns true if function_name exists in the REAPER API
## APITest
```
reaper.APITest()
```

Displays a message window if the API was successfully called.
## ApplyNudge
```
boolean reaper.ApplyNudge(ReaProject project, integer nudgeflag, integer nudgewhat, integer nudgeunits, number value, boolean reverse, integer copies)
```

nudgeflag: &1=set to value (otherwise nudge by value), &2=snap
nudgewhat: 0=position, 1=left trim, 2=left edge, 3=right edge, 4=contents, 5=duplicate, 6=edit cursor
nudgeunit: 0=ms, 1=seconds, 2=grid, 3=256th notes, ..., 15=whole notes, 16=measures.beats (1.15 = 1 measure + 1.5 beats), 17=samples, 18=frames, 19=pixels, 20=item lengths, 21=item selections
value: amount to nudge by, or value to set to
reverse: in nudge mode, nudges left (otherwise ignored)
copies: in nudge duplicate mode, number of copies (otherwise ignored)
## ArmCommand
```
reaper.ArmCommand(integer cmd, string sectionname)
```

arms a command (or disarms if 0 passed) in section sectionname (empty string for main)
## Audio_Init
```
reaper.Audio_Init()
```

open all audio and MIDI devices, if not open
## Audio_IsPreBuffer
```
integer reaper.Audio_IsPreBuffer()
```

is in pre-buffer? threadsafe
## Audio_IsRunning
```
integer reaper.Audio_IsRunning()
```

is audio running at all? threadsafe
## Audio_Quit
```
reaper.Audio_Quit()
```

close all audio and MIDI devices, if open
## AudioAccessorStateChanged
```
boolean reaper.AudioAccessorStateChanged(AudioAccessor accessor)
```

Returns true if the underlying samples (track or media item take) have changed, but does not update the audio accessor, so the user can selectively call AudioAccessorValidateState only when needed. See CreateTakeAudioAccessor, CreateTrackAudioAccessor, DestroyAudioAccessor, GetAudioAccessorEndTime, GetAudioAccessorSamples.
## AudioAccessorUpdate
```
reaper.AudioAccessorUpdate(AudioAccessor accessor)
```

Force the accessor to reload its state from the underlying track or media item take. See CreateTakeAudioAccessor, CreateTrackAudioAccessor, DestroyAudioAccessor, AudioAccessorStateChanged, GetAudioAccessorStartTime, GetAudioAccessorEndTime, GetAudioAccessorSamples.
## AudioAccessorValidateState
```
boolean reaper.AudioAccessorValidateState(AudioAccessor accessor)
```

Validates the current state of the audio accessor -- must ONLY call this from the main thread. Returns true if the state changed.
## BypassFxAllTracks
```
reaper.BypassFxAllTracks(integer bypass)
```

-1 = bypass all if not all bypassed,otherwise unbypass all
## CalcMediaSrcLoudness
```
integer reaper.CalcMediaSrcLoudness(PCM_source mediasource)
```

Calculates loudness statistics of media via dry run render. Statistics will be displayed to the user; call GetSetProjectInfo_String("RENDER_STATS") to retrieve via API. Returns 1 if loudness was calculated successfully, -1 if user canceled the dry run render.
## CalculateNormalization
```
number reaper.CalculateNormalization(PCM_source source, integer normalizeTo, number normalizeTarget, number normalizeStart, number normalizeEnd)
```

Calculate normalize adjustment for source media. normalizeTo: 0=LUFS-I, 1=RMS-I, 2=peak, 3=true peak, 4=LUFS-M max, 5=LUFS-S max. normalizeTarget: dBFS or LUFS value. normalizeStart, normalizeEnd: time bounds within source media for normalization calculation. If normalizationStart=0 and normalizationEnd=0, the full duration of the media will be used for the calculation.
## ClearAllRecArmed
```
reaper.ClearAllRecArmed()
```

No description available.
## ClearConsole
```
reaper.ClearConsole()
```

Clear the ReaScript console. See ShowConsoleMsg
## ClearPeakCache
```
reaper.ClearPeakCache()
```

resets the global peak caches
## ColorFromNative
```
integer r, integer g, integer b = reaper.ColorFromNative(integer col)
```

Extract RGB values from an OS dependent color. See ColorToNative.
## ColorToNative
```
integer reaper.ColorToNative(integer r, integer g, integer b)
```

Make an OS dependent color from RGB values (e.g. RGB() macro on Windows). r,g and b are in [0..255]. See ColorFromNative.
## CountActionShortcuts
```
integer reaper.CountActionShortcuts(KbdSectionInfo section, integer cmdID)
```

Returns the number of shortcuts that exist for the given command ID.
see GetActionShortcutDesc, DeleteActionShortcut, DoActionShortcutDialog.
## CountAutomationItems
```
integer reaper.CountAutomationItems(TrackEnvelope env)
```

Returns the number of automation items on this envelope. See GetSetAutomationItemInfo
## CountEnvelopePoints
```
integer reaper.CountEnvelopePoints(TrackEnvelope envelope)
```

Returns the number of points in the envelope. See CountEnvelopePointsEx.
## CountEnvelopePointsEx
```
integer reaper.CountEnvelopePointsEx(TrackEnvelope envelope, integer autoitem_idx)
```

Returns the number of points in the envelope.
autoitem_idx=-1 for the underlying envelope, 0 for the first automation item on the envelope, etc.
For automation items, pass autoitem_idx|0x10000000 to base ptidx on the number of points in one full loop iteration,
even if the automation item is trimmed so that not all points are visible.
Otherwise, ptidx will be based on the number of visible points in the automation item, including all loop iterations.
See GetEnvelopePointEx, SetEnvelopePointEx, InsertEnvelopePointEx, DeleteEnvelopePointEx.
## CountMediaItems
```
integer reaper.CountMediaItems(ReaProject proj)
```

count the number of items in the project (proj=0 for active project)
## CountProjectMarkers
```
integer retval, integer num_markers, integer num_regions = reaper.CountProjectMarkers(ReaProject proj)
```

num_markersOut and num_regionsOut may be NULL.
## CountSelectedMediaItems
```
integer reaper.CountSelectedMediaItems(ReaProject proj)
```

Discouraged, because GetSelectedMediaItem can be inefficient if media items are added, rearranged, or deleted in between calls. Instead see CountMediaItems, GetMediaItem, IsMediaItemSelected.
## CountSelectedTracks
```
integer reaper.CountSelectedTracks(ReaProject proj)
```

Count the number of selected tracks in the project (proj=0 for active project). This function ignores the master track, see CountSelectedTracks2.
## CountSelectedTracks2
```
integer reaper.CountSelectedTracks2(ReaProject proj, boolean wantmaster)
```

Count the number of selected tracks in the project (proj=0 for active project).
## CountTakeEnvelopes
```
integer reaper.CountTakeEnvelopes(MediaItem_Take take)
```

See GetTakeEnvelope
## CountTakes
```
integer reaper.CountTakes(MediaItem item)
```

count the number of takes in the item
## CountTCPFXParms
```
integer reaper.CountTCPFXParms(ReaProject project, MediaTrack track)
```

Count the number of FX parameter knobs displayed on the track control panel.
## CountTempoTimeSigMarkers
```
integer reaper.CountTempoTimeSigMarkers(ReaProject proj)
```

Count the number of tempo/time signature markers in the project. See GetTempoTimeSigMarker, SetTempoTimeSigMarker, AddTempoTimeSigMarker.
## CountTrackEnvelopes
```
integer reaper.CountTrackEnvelopes(MediaTrack track)
```

see GetTrackEnvelope
## CountTrackMediaItems
```
integer reaper.CountTrackMediaItems(MediaTrack track)
```

count the number of items in the track
## CountTracks
```
integer reaper.CountTracks(ReaProject proj)
```

count the number of tracks in the project (proj=0 for active project)
## CreateNewMIDIItemInProj
```
MediaItem reaper.CreateNewMIDIItemInProj(MediaTrack track, number starttime, number endtime, optional boolean qnIn)
```

Create a new MIDI media item, containing no MIDI events. Time is in seconds unless qn is set.
## CreateTakeAudioAccessor
```
AudioAccessor reaper.CreateTakeAudioAccessor(MediaItem_Take take)
```

Create an audio accessor object for this take. Must only call from the main thread. See CreateTrackAudioAccessor, DestroyAudioAccessor, AudioAccessorStateChanged, GetAudioAccessorStartTime, GetAudioAccessorEndTime, GetAudioAccessorSamples.
## CreateTrackAudioAccessor
```
AudioAccessor reaper.CreateTrackAudioAccessor(MediaTrack track)
```

Create an audio accessor object for this track. Must only call from the main thread. See CreateTakeAudioAccessor, DestroyAudioAccessor, AudioAccessorStateChanged, GetAudioAccessorStartTime, GetAudioAccessorEndTime, GetAudioAccessorSamples.
## CreateTrackSend
```
integer reaper.CreateTrackSend(MediaTrack tr, MediaTrack desttrIn)
```

Create a send/receive (desttrInOptional!=NULL), or a hardware output (desttrInOptional==NULL) with default properties, return >=0 on success (== new send/receive index). See RemoveTrackSend, GetSetTrackSendInfo, GetTrackSendInfo_Value, SetTrackSendInfo_Value.
## CSurf_FlushUndo
```
reaper.CSurf_FlushUndo(boolean force)
```

call this to force flushing of the undo states after using CSurf_On*Change()
## CSurf_GetTouchState
```
boolean reaper.CSurf_GetTouchState(MediaTrack trackid, integer isPan)
```

No description available.
## CSurf_GoEnd
```
reaper.CSurf_GoEnd()
```

No description available.
## CSurf_GoStart
```
reaper.CSurf_GoStart()
```

No description available.
## CSurf_NumTracks
```
integer reaper.CSurf_NumTracks(boolean mcpView)
```

No description available.
## CSurf_OnArrow
```
reaper.CSurf_OnArrow(integer whichdir, boolean wantzoom)
```

No description available.
## CSurf_OnFwd
```
reaper.CSurf_OnFwd(integer seekplay)
```

No description available.
## CSurf_OnFXChange
```
boolean reaper.CSurf_OnFXChange(MediaTrack trackid, integer en)
```

No description available.
## CSurf_OnInputMonitorChange
```
integer reaper.CSurf_OnInputMonitorChange(MediaTrack trackid, integer monitor)
```

No description available.
## CSurf_OnInputMonitorChangeEx
```
integer reaper.CSurf_OnInputMonitorChangeEx(MediaTrack trackid, integer monitor, boolean allowgang)
```

No description available.
## CSurf_OnMuteChange
```
boolean reaper.CSurf_OnMuteChange(MediaTrack trackid, integer mute)
```

No description available.
## CSurf_OnMuteChangeEx
```
boolean reaper.CSurf_OnMuteChangeEx(MediaTrack trackid, integer mute, boolean allowgang)
```

No description available.
## CSurf_OnPanChange
```
number reaper.CSurf_OnPanChange(MediaTrack trackid, number pan, boolean relative)
```

No description available.
## CSurf_OnPanChangeEx
```
number reaper.CSurf_OnPanChangeEx(MediaTrack trackid, number pan, boolean relative, boolean allowGang)
```

No description available.
## CSurf_OnPause
```
reaper.CSurf_OnPause()
```

No description available.
## CSurf_OnPlay
```
reaper.CSurf_OnPlay()
```

No description available.
## CSurf_OnPlayRateChange
```
reaper.CSurf_OnPlayRateChange(number playrate)
```

No description available.
## CSurf_OnRecArmChange
```
boolean reaper.CSurf_OnRecArmChange(MediaTrack trackid, integer recarm)
```

No description available.
## CSurf_OnRecArmChangeEx
```
boolean reaper.CSurf_OnRecArmChangeEx(MediaTrack trackid, integer recarm, boolean allowgang)
```

No description available.
## CSurf_OnRecord
```
reaper.CSurf_OnRecord()
```

No description available.
## CSurf_OnRecvPanChange
```
number reaper.CSurf_OnRecvPanChange(MediaTrack trackid, integer recv_index, number pan, boolean relative)
```

No description available.
## CSurf_OnRecvVolumeChange
```
number reaper.CSurf_OnRecvVolumeChange(MediaTrack trackid, integer recv_index, number volume, boolean relative)
```

No description available.
## CSurf_OnRew
```
reaper.CSurf_OnRew(integer seekplay)
```

No description available.
## CSurf_OnRewFwd
```
reaper.CSurf_OnRewFwd(integer seekplay, integer dir)
```

No description available.
## CSurf_OnScroll
```
reaper.CSurf_OnScroll(integer xdir, integer ydir)
```

No description available.
## CSurf_OnSelectedChange
```
boolean reaper.CSurf_OnSelectedChange(MediaTrack trackid, integer selected)
```

No description available.
## CSurf_OnSendPanChange
```
number reaper.CSurf_OnSendPanChange(MediaTrack trackid, integer send_index, number pan, boolean relative)
```

No description available.
## CSurf_OnSendVolumeChange
```
number reaper.CSurf_OnSendVolumeChange(MediaTrack trackid, integer send_index, number volume, boolean relative)
```

No description available.
## CSurf_OnSoloChange
```
boolean reaper.CSurf_OnSoloChange(MediaTrack trackid, integer solo)
```

No description available.
## CSurf_OnSoloChangeEx
```
boolean reaper.CSurf_OnSoloChangeEx(MediaTrack trackid, integer solo, boolean allowgang)
```

No description available.
## CSurf_OnStop
```
reaper.CSurf_OnStop()
```

No description available.
## CSurf_OnTempoChange
```
reaper.CSurf_OnTempoChange(number bpm)
```

No description available.
## CSurf_OnTrackSelection
```
reaper.CSurf_OnTrackSelection(MediaTrack trackid)
```

No description available.
## CSurf_OnVolumeChange
```
number reaper.CSurf_OnVolumeChange(MediaTrack trackid, number volume, boolean relative)
```

No description available.
## CSurf_OnVolumeChangeEx
```
number reaper.CSurf_OnVolumeChangeEx(MediaTrack trackid, number volume, boolean relative, boolean allowGang)
```

No description available.
## CSurf_OnWidthChange
```
number reaper.CSurf_OnWidthChange(MediaTrack trackid, number width, boolean relative)
```

No description available.
## CSurf_OnWidthChangeEx
```
number reaper.CSurf_OnWidthChangeEx(MediaTrack trackid, number width, boolean relative, boolean allowGang)
```

No description available.
## CSurf_OnZoom
```
reaper.CSurf_OnZoom(integer xdir, integer ydir)
```

No description available.
## CSurf_ResetAllCachedVolPanStates
```
reaper.CSurf_ResetAllCachedVolPanStates()
```

No description available.
## CSurf_ScrubAmt
```
reaper.CSurf_ScrubAmt(number amt)
```

No description available.
## CSurf_SetAutoMode
```
reaper.CSurf_SetAutoMode(integer mode, IReaperControlSurface ignoresurf)
```

No description available.
## CSurf_SetPlayState
```
reaper.CSurf_SetPlayState(boolean play, boolean pause, boolean rec, IReaperControlSurface ignoresurf)
```

No description available.
## CSurf_SetRepeatState
```
reaper.CSurf_SetRepeatState(boolean rep, IReaperControlSurface ignoresurf)
```

No description available.
## CSurf_SetSurfaceMute
```
reaper.CSurf_SetSurfaceMute(MediaTrack trackid, boolean mute, IReaperControlSurface ignoresurf)
```

No description available.
## CSurf_SetSurfacePan
```
reaper.CSurf_SetSurfacePan(MediaTrack trackid, number pan, IReaperControlSurface ignoresurf)
```

No description available.
## CSurf_SetSurfaceRecArm
```
reaper.CSurf_SetSurfaceRecArm(MediaTrack trackid, boolean recarm, IReaperControlSurface ignoresurf)
```

No description available.
## CSurf_SetSurfaceSelected
```
reaper.CSurf_SetSurfaceSelected(MediaTrack trackid, boolean selected, IReaperControlSurface ignoresurf)
```

No description available.
## CSurf_SetSurfaceSolo
```
reaper.CSurf_SetSurfaceSolo(MediaTrack trackid, boolean solo, IReaperControlSurface ignoresurf)
```

No description available.
## CSurf_SetSurfaceVolume
```
reaper.CSurf_SetSurfaceVolume(MediaTrack trackid, number volume, IReaperControlSurface ignoresurf)
```

No description available.
## CSurf_SetTrackListChange
```
reaper.CSurf_SetTrackListChange()
```

No description available.
## CSurf_TrackFromID
```
MediaTrack reaper.CSurf_TrackFromID(integer idx, boolean mcpView)
```

No description available.
## CSurf_TrackToID
```
integer reaper.CSurf_TrackToID(MediaTrack track, boolean mcpView)
```

No description available.
## DB2SLIDER
```
number reaper.DB2SLIDER(number x)
```

No description available.
## DeleteActionShortcut
```
boolean reaper.DeleteActionShortcut(KbdSectionInfo section, integer cmdID, integer shortcutidx)
```

Delete the specific shortcut for the given command ID.
See CountActionShortcuts, GetActionShortcutDesc, DoActionShortcutDialog.
## DeleteEnvelopePointEx
```
boolean reaper.DeleteEnvelopePointEx(TrackEnvelope envelope, integer autoitem_idx, integer ptidx)
```

Delete an envelope point. If setting multiple points at once, set noSort=true, and call Envelope_SortPoints when done.
autoitem_idx=-1 for the underlying envelope, 0 for the first automation item on the envelope, etc.
For automation items, pass autoitem_idx|0x10000000 to base ptidx on the number of points in one full loop iteration,
even if the automation item is trimmed so that not all points are visible.
Otherwise, ptidx will be based on the number of visible points in the automation item, including all loop iterations.
See CountEnvelopePointsEx, GetEnvelopePointEx, SetEnvelopePointEx, InsertEnvelopePointEx.
## DeleteEnvelopePointRange
```
boolean reaper.DeleteEnvelopePointRange(TrackEnvelope envelope, number time_start, number time_end)
```

Delete a range of envelope points. See DeleteEnvelopePointRangeEx, DeleteEnvelopePointEx.
## DeleteEnvelopePointRangeEx
```
boolean reaper.DeleteEnvelopePointRangeEx(TrackEnvelope envelope, integer autoitem_idx, number time_start, number time_end)
```

Delete a range of envelope points. autoitem_idx=-1 for the underlying envelope, 0 for the first automation item on the envelope, etc.
## DeleteExtState
```
reaper.DeleteExtState(string section, string key, boolean persist)
```

Delete the extended state value for a specific section and key. persist=true means the value should remain deleted the next time REAPER is opened. See SetExtState, GetExtState, HasExtState.
## DeleteProjectMarker
```
boolean reaper.DeleteProjectMarker(ReaProject proj, integer markrgnindexnumber, boolean isrgn)
```

Delete a marker. proj==NULL for the active project.
## DeleteProjectMarkerByIndex
```
boolean reaper.DeleteProjectMarkerByIndex(ReaProject proj, integer markrgnidx)
```

Differs from DeleteProjectMarker only in that markrgnidx is 0 for the first marker/region, 1 for the next, etc (see EnumProjectMarkers3), rather than representing the displayed marker/region ID number (see SetProjectMarker4).
## DeleteTakeMarker
```
boolean reaper.DeleteTakeMarker(MediaItem_Take take, integer idx)
```

Delete a take marker. Note that idx will change for all following take markers. See GetNumTakeMarkers, GetTakeMarker, SetTakeMarker
## DeleteTakeStretchMarkers
```
integer reaper.DeleteTakeStretchMarkers(MediaItem_Take take, integer idx, optional integer countIn)
```

Deletes one or more stretch markers. Returns number of stretch markers deleted.
## DeleteTempoTimeSigMarker
```
boolean reaper.DeleteTempoTimeSigMarker(ReaProject project, integer markerindex)
```

Delete a tempo/time signature marker.
## DeleteTrack
```
reaper.DeleteTrack(MediaTrack tr)
```

deletes a track
## DeleteTrackMediaItem
```
boolean reaper.DeleteTrackMediaItem(MediaTrack tr, MediaItem it)
```

No description available.
## DestroyAudioAccessor
```
reaper.DestroyAudioAccessor(AudioAccessor accessor)
```

Destroy an audio accessor. Must only call from the main thread. See CreateTakeAudioAccessor, CreateTrackAudioAccessor, AudioAccessorStateChanged, GetAudioAccessorStartTime, GetAudioAccessorEndTime, GetAudioAccessorSamples.
## DoActionShortcutDialog
```
boolean reaper.DoActionShortcutDialog(HWND hwnd, KbdSectionInfo section, integer cmdID, integer shortcutidx)
```

Open the action shortcut dialog to edit or add a shortcut for the given command ID. If (shortcutidx >= 0 && shortcutidx < CountActionShortcuts()), that specific shortcut will be replaced, otherwise a new shortcut will be added.
See CountActionShortcuts, GetActionShortcutDesc, DeleteActionShortcut.
## Dock_UpdateDockID
```
reaper.Dock_UpdateDockID(string ident_str, integer whichDock)
```

updates preference for docker window ident_str to be in dock whichDock on next open
## DockGetPosition
```
integer reaper.DockGetPosition(integer whichDock)
```

-1=not found, 0=bottom, 1=left, 2=top, 3=right, 4=floating
## DockIsChildOfDock
```
integer retval, boolean isFloatingDocker = reaper.DockIsChildOfDock(HWND hwnd)
```

returns dock index that contains hwnd, or -1
## DockWindowActivate
```
reaper.DockWindowActivate(HWND hwnd)
```

No description available.
## DockWindowAdd
```
reaper.DockWindowAdd(HWND hwnd, string name, integer pos, boolean allowShow)
```

No description available.
## DockWindowAddEx
```
reaper.DockWindowAddEx(HWND hwnd, string name, string identstr, boolean allowShow)
```

No description available.
## DockWindowRefresh
```
reaper.DockWindowRefresh()
```

No description available.
## DockWindowRefreshForHWND
```
reaper.DockWindowRefreshForHWND(HWND hwnd)
```

No description available.
## DockWindowRemove
```
reaper.DockWindowRemove(HWND hwnd)
```

No description available.
## EditTempoTimeSigMarker
```
boolean reaper.EditTempoTimeSigMarker(ReaProject project, integer markerindex)
```

Open the tempo/time signature marker editor dialog.
## EnsureNotCompletelyOffscreen
```
integerr.left, integerr.top, integerr.right, integerr.bot = reaper.EnsureNotCompletelyOffscreen(integerr.left, integerr.top, integerr.right, integerr.bot)
```

call with a saved window rect for your window and it'll correct any positioning info.
## EnumerateFiles
```
string reaper.EnumerateFiles(string path, integer fileindex)
```

List the files in the "path" directory. Returns NULL/nil when all files have been listed. Use fileindex = -1 to force re-read of directory (invalidate cache). See EnumerateSubdirectories
## EnumerateSubdirectories
```
string reaper.EnumerateSubdirectories(string path, integer subdirindex)
```

List the subdirectories in the "path" directory. Use subdirindex = -1 to force re-read of directory (invalidate cache). Returns NULL/nil when all subdirectories have been listed. See EnumerateFiles
## EnumInstalledFX
```
boolean retval, string name, string ident = reaper.EnumInstalledFX(integer index)
```

Enumerates installed FX. Returns true if successful, sets nameOut and identOut to name and ident of FX at index.
## EnumPitchShiftModes
```
boolean retval, string str = reaper.EnumPitchShiftModes(integer mode)
```

Start querying modes at 0, returns FALSE when no more modes possible, sets strOut to NULL if a mode is currently unsupported
## EnumPitchShiftSubModes
```
string reaper.EnumPitchShiftSubModes(integer mode, integer submode)
```

Returns submode name, or NULL
## EnumProjectMarkers
```
integer retval, boolean isrgn, number pos, number rgnend, string name, integer markrgnindexnumber = reaper.EnumProjectMarkers(integer idx)
```

No description available.
## EnumProjectMarkers2
```
integer retval, boolean isrgn, number pos, number rgnend, string name, integer markrgnindexnumber = reaper.EnumProjectMarkers2(ReaProject proj, integer idx)
```

No description available.
## EnumProjectMarkers3
```
integer retval, boolean isrgn, number pos, number rgnend, string name, integer markrgnindexnumber, integer color = reaper.EnumProjectMarkers3(ReaProject proj, integer idx)
```

No description available.
## EnumProjects
```
ReaProject retval, optional string projfn = reaper.EnumProjects(integer idx)
```

idx=-1 for current project,projfn can be NULL if not interested in filename. use idx 0x40000000 for currently rendering project, if any.
## EnumProjExtState
```
boolean retval, optional string key, optional string val = reaper.EnumProjExtState(ReaProject proj, string extname, integer idx)
```

Enumerate the data stored with the project for a specific extname. Returns false when there is no more data. See SetProjExtState, GetProjExtState.
## EnumRegionRenderMatrix
```
MediaTrack reaper.EnumRegionRenderMatrix(ReaProject proj, integer regionindex, integer rendertrack)
```

Enumerate which tracks will be rendered within this region when using the region render matrix. When called with rendertrack==0, the function returns the first track that will be rendered (which may be the master track); rendertrack==1 will return the next track rendered, and so on. The function returns NULL when there are no more tracks that will be rendered within this region.
## EnumTrackMIDIProgramNames
```
boolean retval, string programName = reaper.EnumTrackMIDIProgramNames(integer track, integer programNumber, string programName)
```

returns false if there are no plugins on the track that support MIDI programs,or if all programs have been enumerated
## EnumTrackMIDIProgramNamesEx
```
boolean retval, string programName = reaper.EnumTrackMIDIProgramNamesEx(ReaProject proj, MediaTrack track, integer programNumber, string programName)
```

returns false if there are no plugins on the track that support MIDI programs,or if all programs have been enumerated
## Envelope_Evaluate
```
integer retval, number value, number dVdS, number ddVdS, number dddVdS = reaper.Envelope_Evaluate(TrackEnvelope envelope, number time, number samplerate, integer samplesRequested)
```

Get the effective envelope value at a given time position. samplesRequested is how long the caller expects until the next call to Envelope_Evaluate (often, the buffer block size). The return value is how many samples beyond that time position that the returned values are valid. dVdS is the change in value per sample (first derivative), ddVdS is the second derivative, dddVdS is the third derivative. See GetEnvelopeScalingMode.
## Envelope_FormatValue
```
string buf = reaper.Envelope_FormatValue(TrackEnvelope env, number value)
```

Formats the value of an envelope to a user-readable form
## Envelope_GetParentTake
```
MediaItem_Take retval, integer index, integer index2 = reaper.Envelope_GetParentTake(TrackEnvelope env)
```

If take envelope, gets the take from the envelope. If FX, indexOut set to FX index, index2Out set to parameter index, otherwise -1.
## Envelope_GetParentTrack
```
MediaTrack retval, integer index, integer index2 = reaper.Envelope_GetParentTrack(TrackEnvelope env)
```

If track envelope, gets the track from the envelope. If FX, indexOut set to FX index, index2Out set to parameter index, otherwise -1.
## Envelope_SortPoints
```
boolean reaper.Envelope_SortPoints(TrackEnvelope envelope)
```

Sort envelope points by time. See SetEnvelopePoint, InsertEnvelopePoint.
## Envelope_SortPointsEx
```
boolean reaper.Envelope_SortPointsEx(TrackEnvelope envelope, integer autoitem_idx)
```

Sort envelope points by time. autoitem_idx=-1 for the underlying envelope, 0 for the first automation item on the envelope, etc. See SetEnvelopePoint, InsertEnvelopePoint.
## ExecProcess
```
string reaper.ExecProcess(string cmdline, integer timeoutmsec)
```

Executes command line, returns NULL on total failure, otherwise the return value, a newline, and then the output of the command. If timeoutmsec is 0, command will be allowed to run indefinitely (recommended for large amounts of returned output). timeoutmsec is -1 for no wait/terminate, -2 for no wait and minimize
## file_exists
```
boolean reaper.file_exists(string path)
```

returns true if path points to a valid, readable file
## FindTempoTimeSigMarker
```
integer reaper.FindTempoTimeSigMarker(ReaProject project, number time)
```

Find the tempo/time signature marker that falls at or before this time position (the marker that is in effect as of this time position).
## format_timestr
```
string buf = reaper.format_timestr(number tpos, string buf)
```

Format tpos (which is time in seconds) as hh:mm:ss.sss. See format_timestr_pos, format_timestr_len.
## format_timestr_len
```
string buf = reaper.format_timestr_len(number tpos, string buf, number offset, integer modeoverride)
```

time formatting mode overrides: -1=proj default.
0=time
1=measures.beats + time
2=measures.beats
3=seconds
4=samples
5=h:m:s:f
offset is start of where the length will be calculated from
## format_timestr_pos
```
string buf = reaper.format_timestr_pos(number tpos, string buf, integer modeoverride)
```

time formatting mode overrides: -1=proj default.
0=time
1=measures.beats + time
2=measures.beats
3=seconds
4=samples
5=h:m:s:f
## genGuid
```
string gGUID = reaper.genGuid(string gGUID)
```

No description available.
## get_config_var_string
```
boolean retval, string buf = reaper.get_config_var_string(string name)
```

gets ini configuration variable value as string
## get_ini_file
```
string reaper.get_ini_file()
```

Get reaper.ini full filename.
## GetActionShortcutDesc
```
boolean retval, string desc = reaper.GetActionShortcutDesc(KbdSectionInfo section, integer cmdID, integer shortcutidx)
```

Get the text description of a specific shortcut for the given command ID.
See CountActionShortcuts,DeleteActionShortcut,DoActionShortcutDialog.
## GetActiveTake
```
MediaItem_Take reaper.GetActiveTake(MediaItem item)
```

get the active take in this item
## GetAllProjectPlayStates
```
integer reaper.GetAllProjectPlayStates(ReaProject ignoreProject)
```

returns the bitwise OR of all project play states (1=playing, 2=pause, 4=recording)
## GetAppVersion
```
string reaper.GetAppVersion()
```

Returns app version which may include an OS/arch signifier, such as: "6.17" (windows 32-bit), "6.17/x64" (windows 64-bit), "6.17/OSX64" (macOS 64-bit Intel), "6.17/OSX" (macOS 32-bit), "6.17/macOS-arm64", "6.17/linux-x86_64", "6.17/linux-i686", "6.17/linux-aarch64", "6.17/linux-armv7l", etc
## GetArmedCommand
```
integer retval, string sec = reaper.GetArmedCommand()
```

gets the currently armed command and section name (returns 0 if nothing armed). section name is empty-string for main section.
## GetAudioAccessorEndTime
```
number reaper.GetAudioAccessorEndTime(AudioAccessor accessor)
```

Get the end time of the audio that can be returned from this accessor. See CreateTakeAudioAccessor, CreateTrackAudioAccessor, DestroyAudioAccessor, AudioAccessorStateChanged, GetAudioAccessorStartTime, GetAudioAccessorSamples.
## GetAudioAccessorHash
```
string hashNeed128 = reaper.GetAudioAccessorHash(AudioAccessor accessor, string hashNeed128)
```

Deprecated. See AudioAccessorStateChanged instead.
## GetAudioAccessorSamples
```
integer reaper.GetAudioAccessorSamples(AudioAccessor accessor, integer samplerate, integer numchannels, number starttime_sec, integer numsamplesperchannel, reaper.array samplebuffer)
```

Get a block of samples from the audio accessor. Samples are extracted immediately pre-FX, and returned interleaved (first sample of first channel, first sample of second channel...). Returns 0 if no audio, 1 if audio, -1 on error. See CreateTakeAudioAccessor, CreateTrackAudioAccessor, DestroyAudioAccessor, AudioAccessorStateChanged, GetAudioAccessorStartTime, GetAudioAccessorEndTime.
## GetAudioAccessorStartTime
```
number reaper.GetAudioAccessorStartTime(AudioAccessor accessor)
```

Get the start time of the audio that can be returned from this accessor. See CreateTakeAudioAccessor, CreateTrackAudioAccessor, DestroyAudioAccessor, AudioAccessorStateChanged, GetAudioAccessorEndTime, GetAudioAccessorSamples.
## GetAudioDeviceInfo
```
boolean retval, string desc = reaper.GetAudioDeviceInfo(string attribute)
```

get information about the currently open audio device. attribute can be MODE, IDENT_IN, IDENT_OUT, BSIZE, SRATE, BPS. returns false if unknown attribute or device not open.
## GetConfigWantsDock
```
integer reaper.GetConfigWantsDock(string ident_str)
```

gets the dock ID desired by ident_str, if any
## GetCurrentProjectInLoadSave
```
ReaProject reaper.GetCurrentProjectInLoadSave()
```

returns current project if in load/save (usually only used from project_config_extension_t)
## GetCursorContext
```
integer reaper.GetCursorContext()
```

return the current cursor context: 0 if track panels, 1 if items, 2 if envelopes, otherwise unknown
## GetCursorContext2
```
integer reaper.GetCursorContext2(boolean want_last_valid)
```

0 if track panels, 1 if items, 2 if envelopes, otherwise unknown (unlikely when want_last_valid is true)
## GetCursorPosition
```
number reaper.GetCursorPosition()
```

edit cursor position
## GetCursorPositionEx
```
number reaper.GetCursorPositionEx(ReaProject proj)
```

edit cursor position
## GetDisplayedMediaItemColor
```
integer reaper.GetDisplayedMediaItemColor(MediaItem item)
```

see GetDisplayedMediaItemColor2.
## GetDisplayedMediaItemColor2
```
integer reaper.GetDisplayedMediaItemColor2(MediaItem item, MediaItem_Take take)
```

Returns the custom take, item, or track color that is used (according to the user preference) to color the media item. The returned color is OS dependent|0x01000000 (i.e. ColorToNative(r,g,b)|0x01000000), so a return of zero means "no color", not black.
## GetEnvelopeInfo_Value
```
number reaper.GetEnvelopeInfo_Value(TrackEnvelope env, string parmname)
```

Gets an envelope numerical-value attribute:
I_TCPY : int : Y offset of envelope relative to parent track (may be separate lane or overlap with track contents)
I_TCPH : int : visible height of envelope
I_TCPY_USED : int : Y offset of envelope relative to parent track, exclusive of padding
I_TCPH_USED : int : visible height of envelope, exclusive of padding
P_TRACK : MediaTrack * : parent track pointer (if any)
P_DESTTRACK : MediaTrack * : destination track pointer, if on a send
P_ITEM : MediaItem * : parent item pointer (if any)
P_TAKE : MediaItem_Take * : parent take pointer (if any)
I_SEND_IDX : int : 1-based index of send in P_TRACK, or 0 if not a send
I_HWOUT_IDX : int : 1-based index of hardware output in P_TRACK or 0 if not a hardware output
I_RECV_IDX : int : 1-based index of receive in P_DESTTRACK or 0 if not a send/receive
## GetEnvelopeName
```
boolean retval, string buf = reaper.GetEnvelopeName(TrackEnvelope env)
```

No description available.
## GetEnvelopePoint
```
boolean retval, number time, number value, integer shape, number tension, boolean selected = reaper.GetEnvelopePoint(TrackEnvelope envelope, integer ptidx)
```

Get the attributes of an envelope point. See GetEnvelopePointEx.
## GetEnvelopePointByTime
```
integer reaper.GetEnvelopePointByTime(TrackEnvelope envelope, number time)
```

Returns the envelope point at or immediately prior to the given time position. See GetEnvelopePointByTimeEx.
## GetEnvelopePointByTimeEx
```
integer reaper.GetEnvelopePointByTimeEx(TrackEnvelope envelope, integer autoitem_idx, number time)
```

Returns the envelope point at or immediately prior to the given time position.
autoitem_idx=-1 for the underlying envelope, 0 for the first automation item on the envelope, etc.
For automation items, pass autoitem_idx|0x10000000 to base ptidx on the number of points in one full loop iteration,
even if the automation item is trimmed so that not all points are visible.
Otherwise, ptidx will be based on the number of visible points in the automation item, including all loop iterations.
See GetEnvelopePointEx, SetEnvelopePointEx, InsertEnvelopePointEx, DeleteEnvelopePointEx.
## GetEnvelopePointEx
```
boolean retval, number time, number value, integer shape, number tension, boolean selected = reaper.GetEnvelopePointEx(TrackEnvelope envelope, integer autoitem_idx, integer ptidx)
```

Get the attributes of an envelope point.
autoitem_idx=-1 for the underlying envelope, 0 for the first automation item on the envelope, etc.
For automation items, pass autoitem_idx|0x10000000 to base ptidx on the number of points in one full loop iteration,
even if the automation item is trimmed so that not all points are visible.
Otherwise, ptidx will be based on the number of visible points in the automation item, including all loop iterations.
See CountEnvelopePointsEx, SetEnvelopePointEx, InsertEnvelopePointEx, DeleteEnvelopePointEx.
## GetEnvelopeScalingMode
```
integer reaper.GetEnvelopeScalingMode(TrackEnvelope env)
```

Returns the envelope scaling mode: 0=no scaling, 1=fader scaling. All API functions deal with raw envelope point values, to convert raw from/to scaled values see ScaleFromEnvelopeMode, ScaleToEnvelopeMode.
## GetEnvelopeStateChunk
```
boolean retval, string str = reaper.GetEnvelopeStateChunk(TrackEnvelope env, string str, boolean isundo)
```

Gets the RPPXML state of an envelope, returns true if successful. Undo flag is a performance/caching hint.
## GetEnvelopeUIState
```
integer reaper.GetEnvelopeUIState(TrackEnvelope env)
```

gets information on the UI state of an envelope: returns &1 if automation/modulation is playing back, &2 if automation is being actively written, &4 if the envelope recently had an effective automation mode change
## GetExePath
```
string reaper.GetExePath()
```

returns path of REAPER.exe (not including EXE), i.e. C:\Program Files\REAPER
## GetExtState
```
string reaper.GetExtState(string section, string key)
```

Get the extended state value for a specific section and key. See SetExtState, DeleteExtState, HasExtState.
## GetFocusedFX
```
integer retval, integer tracknumber, integer itemnumber, integer fxnumber = reaper.GetFocusedFX()
```

This function is deprecated (returns GetFocusedFX2()&3), see GetTouchedOrFocusedFX.
## GetFocusedFX2
```
integer retval, integer tracknumber, integer itemnumber, integer fxnumber = reaper.GetFocusedFX2()
```

Return value has 1 set if track FX, 2 if take/item FX, 4 set if FX is no longer focused but still open. tracknumber==0 means the master track, 1 means track 1, etc. itemnumber is zero-based (or -1 if not an item). For interpretation of fxnumber, see GetLastTouchedFX. Deprecated, see GetTouchedOrFocusedFX
## GetFreeDiskSpaceForRecordPath
```
integer reaper.GetFreeDiskSpaceForRecordPath(ReaProject proj, integer pathidx)
```

returns free disk space in megabytes, pathIdx 0 for normal, 1 for alternate.
## GetFXEnvelope
```
TrackEnvelope reaper.GetFXEnvelope(MediaTrack track, integer fxindex, integer parameterindex, boolean create)
```

Returns the FX parameter envelope. If the envelope does not exist and create=true, the envelope will be created. If the envelope already exists and is bypassed and create=true, then the envelope will be unbypassed.
## GetGlobalAutomationOverride
```
integer reaper.GetGlobalAutomationOverride()
```

return -1=no override, 0=trim/read, 1=read, 2=touch, 3=write, 4=latch, 5=bypass
## GetHZoomLevel
```
number reaper.GetHZoomLevel()
```

returns pixels/second
## GetInputActivityLevel
```
number reaper.GetInputActivityLevel(integer input_id)
```

returns approximate input level if available, 0-511 mono inputs, |1024 for stereo pairs, 4096+devidx*32 for MIDI devices
## GetInputChannelName
```
string reaper.GetInputChannelName(integer channelIndex)
```

No description available.
## GetInputOutputLatency
```
integer inputlatency, integer outputLatency = reaper.GetInputOutputLatency()
```

Gets the audio device input/output latency in samples
## GetItemEditingTime2
```
number, PCM_source which_item, integer flags = reaper.GetItemEditingTime2()
```

returns time of relevant edit, set which_item to the pcm_source (if applicable), flags (if specified) will be set to 1 for edge resizing, 2 for fade change, 4 for item move, 8 for item slip edit (edit cursor time or start of item)
## GetItemFromPoint
```
MediaItem, MediaItem_Take take = reaper.GetItemFromPoint(integer screen_x, integer screen_y, boolean allow_locked)
```

Returns the first item at the screen coordinates specified. If allow_locked is false, locked items are ignored. If takeOutOptional specified, returns the take hit. See GetThingFromPoint.
## GetItemProjectContext
```
ReaProject reaper.GetItemProjectContext(MediaItem item)
```

No description available.
## GetItemStateChunk
```
boolean retval, string str = reaper.GetItemStateChunk(MediaItem item, string str, boolean isundo)
```

Gets the RPPXML state of an item, returns true if successful. Undo flag is a performance/caching hint.
## GetLastColorThemeFile
```
string reaper.GetLastColorThemeFile()
```

No description available.
## GetLastMarkerAndCurRegion
```
integer markeridx, integer regionidx = reaper.GetLastMarkerAndCurRegion(ReaProject proj, number time)
```

Get the last project marker before time, and/or the project region that includes time. markeridx and regionidx are returned not necessarily as the displayed marker/region index, but as the index that can be passed to EnumProjectMarkers. Either or both of markeridx and regionidx may be NULL. See EnumProjectMarkers.
## GetLastTouchedFX
```
boolean retval, integer tracknumber, integer fxnumber, integer paramnumber = reaper.GetLastTouchedFX()
```

Returns true if the last touched FX parameter is valid, false otherwise. The low word of tracknumber is the 1-based track index -- 0 means the master track, 1 means track 1, etc. If the high word of tracknumber is nonzero, it refers to the 1-based item index (1 is the first item on the track, etc). For track FX, the low 24 bits of fxnumber refer to the FX index in the chain, and if the next 8 bits are 01, then the FX is record FX. For item FX, the low word defines the FX index in the chain, and the high word defines the take number. Deprecated, see GetTouchedOrFocusedFX.
## GetLastTouchedTrack
```
MediaTrack reaper.GetLastTouchedTrack()
```

No description available.
## GetMainHwnd
```
HWND reaper.GetMainHwnd()
```

No description available.
## GetMasterMuteSoloFlags
```
integer reaper.GetMasterMuteSoloFlags()
```

&1=master mute,&2=master solo. This is deprecated as you can just query the master track as well.
## GetMasterTrack
```
MediaTrack reaper.GetMasterTrack(ReaProject proj)
```

No description available.
## GetMasterTrackVisibility
```
integer reaper.GetMasterTrackVisibility()
```

returns &1 if the master track is visible in the TCP, &2 if NOT visible in the mixer. See SetMasterTrackVisibility.
## GetMaxMidiInputs
```
integer reaper.GetMaxMidiInputs()
```

returns max dev for midi inputs/outputs
## GetMaxMidiOutputs
```
integer reaper.GetMaxMidiOutputs()
```

No description available.
## GetMediaFileMetadata
```
integer retval, string buf = reaper.GetMediaFileMetadata(PCM_source mediaSource, string identifier)
```

Get text-based metadata from a media file for a given identifier. Call with identifier="" to list all identifiers contained in the file, separated by newlines. May return "[Binary data]" for metadata that REAPER doesn't handle.
## GetMediaItem
```
MediaItem reaper.GetMediaItem(ReaProject proj, integer itemidx)
```

get an item from a project by item count (zero-based) (proj=0 for active project)
## GetMediaItem_Track
```
MediaTrack reaper.GetMediaItem_Track(MediaItem item)
```

Get parent track of media item
## GetMediaItemInfo_Value
```
number reaper.GetMediaItemInfo_Value(MediaItem item, string parmname)
```

Get media item numerical-value attributes.
B_MUTE : bool * : muted (item solo overrides). setting this value will clear C_MUTE_SOLO.
B_MUTE_ACTUAL : bool * : muted (ignores solo). setting this value will not affect C_MUTE_SOLO.
C_LANEPLAYS : char * : on fixed lane tracks, 0=this item lane does not play, 1=this item lane plays exclusively, 2=this item lane plays and other lanes also play, -1=this item is on a non-visible, non-playing lane on a formerly fixed-lane track (read-only)
C_MUTE_SOLO : char * : solo override (-1=soloed, 0=no override, 1=unsoloed). note that this API does not automatically unsolo other items when soloing (nor clear the unsolos when clearing the last soloed item), it must be done by the caller via action or via this API.
B_LOOPSRC : bool * : loop source
B_ALLTAKESPLAY : bool * : all takes play
B_UISEL : bool * : selected in arrange view
C_BEATATTACHMODE : char * : item timebase, -1=track or project default, 1=beats (position, length, rate), 2=beats (position only). for auto-stretch timebase: C_BEATATTACHMODE=1, C_AUTOSTRETCH=1
C_AUTOSTRETCH: : char * : auto-stretch at project tempo changes, 1=enabled, requires C_BEATATTACHMODE=1
C_LOCK : char * : locked, &1=locked
D_VOL : double * : item volume, 0=-inf, 0.5=-6dB, 1=+0dB, 2=+6dB, etc
D_POSITION : double * : item position in seconds
D_LENGTH : double * : item length in seconds
D_SNAPOFFSET : double * : item snap offset in seconds
D_FADEINLEN : double * : item manual fadein length in seconds
D_FADEOUTLEN : double * : item manual fadeout length in seconds
D_FADEINDIR : double * : item fadein curvature, -1..1
D_FADEOUTDIR : double * : item fadeout curvature, -1..1
D_FADEINLEN_AUTO : double * : item auto-fadein length in seconds, -1=no auto-fadein
D_FADEOUTLEN_AUTO : double * : item auto-fadeout length in seconds, -1=no auto-fadeout
C_FADEINSHAPE : int * : fadein shape, 0..6, 0=linear
C_FADEOUTSHAPE : int * : fadeout shape, 0..6, 0=linear
I_GROUPID : int * : group ID, 0=no group
I_LASTY : int * : Y-position (relative to top of track) in pixels (read-only)
I_LASTH : int * : height in pixels (read-only)
I_CUSTOMCOLOR : int * : custom color, OS dependent color|0x1000000 (i.e. ColorToNative(r,g,b)|0x1000000). If you do not |0x1000000, then it will not be used, but will store the color
I_CURTAKE : int * : active take number
IP_ITEMNUMBER : int : item number on this track (read-only, returns the item number directly)
F_FREEMODE_Y : float * : free item positioning or fixed lane Y-position. 0=top of track, 1.0=bottom of track
F_FREEMODE_H : float * : free item positioning or fixed lane height. 0.5=half the track height, 1.0=full track height
I_FIXEDLANE : int * : fixed lane of item (fine to call with setNewValue, but returned value is read-only)
B_FIXEDLANE_HIDDEN : bool * : true if displaying only one fixed lane and this item is in a different lane (read-only)
P_TRACK : MediaTrack * : (read-only)
## GetMediaItemNumTakes
```
integer reaper.GetMediaItemNumTakes(MediaItem item)
```

No description available.
## GetMediaItemTake
```
MediaItem_Take reaper.GetMediaItemTake(MediaItem item, integer tk)
```

No description available.
## GetMediaItemTake_Item
```
MediaItem reaper.GetMediaItemTake_Item(MediaItem_Take take)
```

Get parent item of media item take
## GetMediaItemTake_Peaks
```
integer reaper.GetMediaItemTake_Peaks(MediaItem_Take take, number peakrate, number starttime, integer numchannels, integer numsamplesperchannel, integer want_extra_type, reaper.array buf)
```

Gets block of peak samples to buf. Note that the peak samples are interleaved, but in two or three blocks (maximums, then minimums, then extra). Return value has 20 bits of returned sample count, then 4 bits of output_mode (0xf00000), then a bit to signify whether extra_type was available (0x1000000). extra_type can be 115 ('s') for spectral information, which will return peak samples as integers with the low 15 bits frequency, next 14 bits tonality.
## GetMediaItemTake_Source
```
PCM_source reaper.GetMediaItemTake_Source(MediaItem_Take take)
```

Get media source of media item take
## GetMediaItemTake_Track
```
MediaTrack reaper.GetMediaItemTake_Track(MediaItem_Take take)
```

Get parent track of media item take
## GetMediaItemTakeByGUID
```
MediaItem_Take reaper.GetMediaItemTakeByGUID(ReaProject project, string guidGUID)
```

No description available.
## GetMediaItemTakeInfo_Value
```
number reaper.GetMediaItemTakeInfo_Value(MediaItem_Take take, string parmname)
```

Get media item take numerical-value attributes.
D_STARTOFFS : double * : start offset in source media, in seconds
D_VOL : double * : take volume, 0=-inf, 0.5=-6dB, 1=+0dB, 2=+6dB, etc, negative if take polarity is flipped
D_PAN : double * : take pan, -1..1
D_PANLAW : double * : take pan law, -1=default, 0.5=-6dB, 1.0=+0dB, etc
D_PLAYRATE : double * : take playback rate, 0.5=half speed, 1=normal, 2=double speed, etc
D_PITCH : double * : take pitch adjustment in semitones, -12=one octave down, 0=normal, +12=one octave up, etc
B_PPITCH : bool * : preserve pitch when changing playback rate
I_LASTY : int * : Y-position (relative to top of track) in pixels (read-only)
I_LASTH : int * : height in pixels (read-only)
I_CHANMODE : int * : channel mode, 0=normal, 1=reverse stereo, 2=downmix, 3=left, 4=right
I_PITCHMODE : int * : pitch shifter mode, -1=project default, otherwise high 2 bytes=shifter, low 2 bytes=parameter
I_STRETCHFLAGS : int * : stretch marker flags (&7 mask for mode override: 0=default, 1=balanced, 2/3/6=tonal, 4=transient, 5=no pre-echo)
F_STRETCHFADESIZE : float * : stretch marker fade size in seconds (0.0025 default)
I_RECPASSID : int * : record pass ID
I_TAKEFX_NCH : int * : number of internal audio channels for per-take FX to use (OK to call with setNewValue, but the returned value is read-only)
I_CUSTOMCOLOR : int * : custom color, OS dependent color|0x1000000 (i.e. ColorToNative(r,g,b)|0x1000000). If you do not |0x1000000, then it will not be used, but will store the color
IP_SPECEDIT:CNT : int : spectral edit count (read-only)
IP_SPECEDIT:DELETE:x : int : read or write this key to remove the spectral edit specified
IP_SPECEDIT:ADD : int : read or write this key to add a new spectral edit (returns index)
IP_SPECEDIT:SORT : int : read or write this key to re-sort spectral edits (be sure to do this following a position change or insert of new edit)
I_SPECEDIT:FFT_SIZE : int * : FFT size used by spectral edits for this take
D_SPECEDIT:x:POSITION : double * : position of spectral edit start (changing this requires a resort of spectral edits)
D_SPECEDIT:x:LENGTH : double * : length of spectral edit
F_SPECEDIT:x:GAIN : float * : gain of spectral edit
F_SPECEDIT:x:FADE_IN : float * : fade-in size 0..1
F_SPECEDIT:x:FADE_OUT : float * : fade-out size 0..1
F_SPECEDIT:x:FADE_LOW : float * : fade-lf size 0..1
F_SPECEDIT:x:FADE_HI : float * : fade-hf size 0..1
I_SPECEDIT:x:CHAN : int * : channel index, -1 for omni
I_SPECEDIT:x:FLAGS : int * : flags, &1=bypassed, &2=solo
F_SPECEDIT:x:GATE_THRESH : float * : gate threshold
F_SPECEDIT:x:GATE_FLOOR : float * : gate floor
F_SPECEDIT:x:COMP_THRESH : float * : comp threshold
F_SPECEDIT:x:COMP_RATIO : float * : comp ratio
B_SPECEDIT:x:SELECTED : bool * : selection state
I_SPECEDIT:x:TOPFREQ_CNT : int * : (read-only) number of top frequency-points
I_SPECEDIT:x:TOPFREQ_ADD:pos:val : int * : reading or writing will insert top frequency-point with position/value pair, returns index
I_SPECEDIT:x:TOPFREQ_DEL:y : int * : reading or writing will delete top frequency-point y. there will always be at least one point.
F_SPECEDIT:x:TOPFREQ_POS:y : float * : (read-only) get position of top frequency-point y
F_SPECEDIT:x:TOPFREQ_FREQ:y : float * : (read-only) get frequency of top frequency-point y
I_SPECEDIT:x:BOTFREQ_CNT : int * : number of bottom frequency-points
I_SPECEDIT:x:BOTFREQ_ADD:pos:val : int * : reading or writing will insert bottom frequency-point with position/value pair, returns index
I_SPECEDIT:x:BOTFREQ_DEL:y : int * : reading or writing will delete bottom frequency-point y. there will always be at least one point.
F_SPECEDIT:x:BOTFREQ_POS:y : float * : (read-only) get position of bottom frequency-point y
F_SPECEDIT:x:BOTFREQ_FREQ:y : float * : (read-only) get frequency of bottom frequency-point y
IP_TAKENUMBER : int : take number (read-only, returns the take number directly)
P_TRACK : pointer to MediaTrack (read-only)
P_ITEM : pointer to MediaItem (read-only)
P_SOURCE : PCM_source *. Note that if setting this, you should first retrieve the old source, set the new, THEN delete the old.
## GetMediaItemTrack
```
MediaTrack reaper.GetMediaItemTrack(MediaItem item)
```

No description available.
## GetMediaSourceFileName
```
string filenamebuf = reaper.GetMediaSourceFileName(PCM_source source)
```

Copies the media source filename to filenamebuf. Note that in-project MIDI media sources have no associated filename. See GetMediaSourceParent.
## GetMediaSourceLength
```
number retval, boolean lengthIsQN = reaper.GetMediaSourceLength(PCM_source source)
```

Returns the length of the source media. If the media source is beat-based, the length will be in quarter notes, otherwise it will be in seconds.
## GetMediaSourceNumChannels
```
integer reaper.GetMediaSourceNumChannels(PCM_source source)
```

Returns the number of channels in the source media.
## GetMediaSourceParent
```
PCM_source reaper.GetMediaSourceParent(PCM_source src)
```

Returns the parent source, or NULL if src is the root source. This can be used to retrieve the parent properties of sections or reversed sources for example.
## GetMediaSourceSampleRate
```
integer reaper.GetMediaSourceSampleRate(PCM_source source)
```

Returns the sample rate. MIDI source media will return zero.
## GetMediaSourceType
```
string typebuf = reaper.GetMediaSourceType(PCM_source source)
```

copies the media source type ("WAV", "MIDI", etc) to typebuf
## GetMediaTrackInfo_Value
```
number reaper.GetMediaTrackInfo_Value(MediaTrack tr, string parmname)
```

Get track numerical-value attributes.
B_MUTE : bool * : muted
B_PHASE : bool * : track phase inverted
B_RECMON_IN_EFFECT : bool * : record monitoring in effect (current audio-thread playback state, read-only)
IP_TRACKNUMBER : int : track number 1-based, 0=not found, -1=master track (read-only, returns the int directly)
I_SOLO : int * : soloed, 0=not soloed, 1=soloed, 2=soloed in place, 5=safe soloed, 6=safe soloed in place
B_SOLO_DEFEAT : bool * : when set, if anything else is soloed and this track is not muted, this track acts soloed
I_FXEN : int * : fx enabled, 0=bypassed, !0=fx active
I_RECARM : int * : record armed, 0=not record armed, 1=record armed
I_RECINPUT : int * : record input, <0=no input. if 4096 set, input is MIDI and low 5 bits represent channel (0=all, 1-16=only chan), next 6 bits represent physical input (63=all, 62=VKB). If 4096 is not set, low 10 bits (0..1023) are input start channel (ReaRoute/Loopback start at 512). If 2048 is set, input is multichannel input (using track channel count), or if 1024 is set, input is stereo input, otherwise input is mono.
I_RECMODE : int * : record mode, 0=input, 1=stereo out, 2=none, 3=stereo out w/latency compensation, 4=midi output, 5=mono out, 6=mono out w/ latency compensation, 7=midi overdub, 8=midi replace
I_RECMODE_FLAGS : int * : record mode flags, &3=output recording mode (0=post fader, 1=pre-fx, 2=post-fx/pre-fader)
I_RECMON : int * : record monitoring, 0=off, 1=normal, 2=not when playing (tape style)
I_RECMONITEMS : int * : monitor items while recording, 0=off, 1=on
B_AUTO_RECARM : bool * : automatically set record arm when selected (does not immediately affect recarm state, script should set directly if desired)
I_VUMODE : int * : track vu mode, &1:disabled, &30==0:stereo peaks, &30==2:multichannel peaks, &30==4:stereo RMS, &30==8:combined RMS, &30==12:LUFS-M, &30==16:LUFS-S (readout=max), &30==20:LUFS-S (readout=current), &32:LUFS calculation on channels 1+2 only
I_AUTOMODE : int * : track automation mode, 0=trim/off, 1=read, 2=touch, 3=write, 4=latch
I_NCHAN : int * : number of track channels, 2-128, even numbers only
I_SELECTED : int * : track selected, 0=unselected, 1=selected
I_WNDH : int * : current TCP window height in pixels including envelopes (read-only)
I_TCPH : int * : current TCP window height in pixels not including envelopes (read-only)
I_TCPY : int * : current TCP window Y-position in pixels relative to top of arrange view (read-only)
I_MCPX : int * : current MCP X-position in pixels relative to mixer container (read-only)
I_MCPY : int * : current MCP Y-position in pixels relative to mixer container (read-only)
I_MCPW : int * : current MCP width in pixels (read-only)
I_MCPH : int * : current MCP height in pixels (read-only)
I_FOLDERDEPTH : int * : folder depth change, 0=normal, 1=track is a folder parent, -1=track is the last in the innermost folder, -2=track is the last in the innermost and next-innermost folders, etc
I_FOLDERCOMPACT : int * : folder collapsed state (only valid on folders), 0=normal, 1=collapsed, 2=fully collapsed
I_MIDIHWOUT : int * : track midi hardware output index, <0=disabled, low 5 bits are which channels (0=all, 1-16), next 5 bits are output device index (0-31)
I_MIDI_INPUT_CHANMAP : int * : -1 maps to source channel, otherwise 1-16 to map to MIDI channel
I_MIDI_CTL_CHAN : int * : -1 no link, 0-15 link to MIDI volume/pan on channel, 16 link to MIDI volume/pan on all channels
I_MIDI_TRACKSEL_FLAG : int * : MIDI editor track list options: &1=expand media items, &2=exclude from list, &4=auto-pruned
I_PERFFLAGS : int * : track performance flags, &1=no media buffering, &2=no anticipative FX
I_CUSTOMCOLOR : int * : custom color, OS dependent color|0x1000000 (i.e. ColorToNative(r,g,b)|0x1000000). If you do not |0x1000000, then it will not be used, but will store the color
I_HEIGHTOVERRIDE : int * : custom height override for TCP window, 0 for none, otherwise size in pixels
I_SPACER : int * : 1=TCP track spacer above this trackB_HEIGHTLOCK : bool * : track height lock (must set I_HEIGHTOVERRIDE before locking)
D_VOL : double * : trim volume of track, 0=-inf, 0.5=-6dB, 1=+0dB, 2=+6dB, etc
D_PAN : double * : trim pan of track, -1..1
D_WIDTH : double * : width of track, -1..1
D_DUALPANL : double * : dualpan position 1, -1..1, only if I_PANMODE==6
D_DUALPANR : double * : dualpan position 2, -1..1, only if I_PANMODE==6
I_PANMODE : int * : pan mode, 0=classic 3.x, 3=new balance, 5=stereo pan, 6=dual pan
D_PANLAW : double * : pan law of track, <0=project default, 0.5=-6dB, 0.707..=-3dB, 1=+0dB, 1.414..=-3dB with gain compensation, 2=-6dB with gain compensation, etc
I_PANLAW_FLAGS : int * : pan law flags, 0=sine taper, 1=hybrid taper with deprecated behavior when gain compensation enabled, 2=linear taper, 3=hybrid taper
P_ENV:<envchunkname or P_ENV:{GUID... : TrackEnvelope * : (read-only) chunkname can be <VOLENV, <PANENV, etc; GUID is the stringified envelope GUID.
B_SHOWINMIXER : bool * : track control panel visible in mixer (do not use on master track)
B_SHOWINTCP : bool * : track control panel visible in arrange view (do not use on master track)
B_MAINSEND : bool * : track sends audio to parent
C_MAINSEND_OFFS : char * : channel offset of track send to parent
C_MAINSEND_NCH : char * : channel count of track send to parent (0=use all child track channels, 1=use one channel only)
I_FREEMODE : int * : 1=track free item positioning enabled, 2=track fixed lanes enabled (call UpdateTimeline() after changing)
I_NUMFIXEDLANES : int * : number of track fixed lanes (fine to call with setNewValue, but returned value is read-only)
C_LANESCOLLAPSED : char * : fixed lane collapse state (1=lanes collapsed, 2=track displays as non-fixed-lanes but hidden lanes exist)
C_LANESETTINGS : char * : fixed lane settings (&1=auto-remove empty lanes at bottom, &2=do not auto-comp new recording, &4=newly recorded lanes play exclusively (else add lanes in layers), &8=big lanes (else small lanes), &16=add new recording at bottom (else record into first available lane), &32=hide lane buttons
C_LANEPLAYS:N : char * : on fixed lane tracks, 0=lane N does not play, 1=lane N plays exclusively, 2=lane N plays and other lanes also play (fine to call with setNewValue, but returned value is read-only)
C_ALLLANESPLAY : char * : on fixed lane tracks, 0=no lanes play, 1=all lanes play, 2=some lanes play (fine to call with setNewValue 0 or 1, but returned value is read-only)
C_BEATATTACHMODE : char * : track timebase, -1=project default, 0=time, 1=beats (position, length, rate), 2=beats (position only)
F_MCP_FXSEND_SCALE : float * : scale of fx+send area in MCP (0=minimum allowed, 1=maximum allowed)
F_MCP_FXPARM_SCALE : float * : scale of fx parameter area in MCP (0=minimum allowed, 1=maximum allowed)
F_MCP_SENDRGN_SCALE : float * : scale of send area as proportion of the fx+send total area (0=minimum allowed, 1=maximum allowed)
F_TCP_FXPARM_SCALE : float * : scale of TCP parameter area when TCP FX are embedded (0=min allowed, default, 1=max allowed)
I_PLAY_OFFSET_FLAG : int * : track media playback offset state, &1=bypassed, &2=offset value is measured in samples (otherwise measured in seconds)
D_PLAY_OFFSET : double * : track media playback offset, units depend on I_PLAY_OFFSET_FLAG
P_PARTRACK : MediaTrack * : parent track (read-only)
P_PROJECT : ReaProject * : parent project (read-only)
## GetMIDIInputName
```
boolean retval, string nameout = reaper.GetMIDIInputName(integer dev, string nameout)
```

returns true if device present
## GetMIDIOutputName
```
boolean retval, string nameout = reaper.GetMIDIOutputName(integer dev, string nameout)
```

returns true if device present
## GetMixerScroll
```
MediaTrack reaper.GetMixerScroll()
```

Get the leftmost track visible in the mixer
## GetMouseModifier
```
string action = reaper.GetMouseModifier(string context, integer modifier_flag)
```

Get the current mouse modifier assignment for a specific modifier key assignment, in a specific context.
action will be filled in with the command ID number for a built-in mouse modifier
or built-in REAPER command ID, or the custom action ID string.
Note: the action string may have a space and 'c' or 'm' appended to it to specify command ID vs mouse modifier ID.
See SetMouseModifier for more information.
## GetMousePosition
```
integer x, integer y = reaper.GetMousePosition()
```

get mouse position in screen coordinates
## GetNumAudioInputs
```
integer reaper.GetNumAudioInputs()
```

Return number of normal audio hardware inputs available
## GetNumAudioOutputs
```
integer reaper.GetNumAudioOutputs()
```

Return number of normal audio hardware outputs available
## GetNumMIDIInputs
```
integer reaper.GetNumMIDIInputs()
```

returns max number of real midi hardware inputs
## GetNumMIDIOutputs
```
integer reaper.GetNumMIDIOutputs()
```

returns max number of real midi hardware outputs
## GetNumTakeMarkers
```
integer reaper.GetNumTakeMarkers(MediaItem_Take take)
```

Returns number of take markers. See GetTakeMarker, SetTakeMarker, DeleteTakeMarker
## GetNumTracks
```
integer reaper.GetNumTracks()
```

Returns number of tracks in current project, see CountTracks()
## GetOS
```
string reaper.GetOS()
```

Returns "Win32", "Win64", "OSX32", "OSX64", "macOS-arm64", or "Other".
## GetOutputChannelName
```
string reaper.GetOutputChannelName(integer channelIndex)
```

No description available.
## GetOutputLatency
```
number reaper.GetOutputLatency()
```

returns output latency in seconds
## GetParentTrack
```
MediaTrack reaper.GetParentTrack(MediaTrack track)
```

No description available.
## GetPeakFileName
```
string buf = reaper.GetPeakFileName(string fn)
```

get the peak file name for a given file (can be either filename.reapeaks,or a hashed filename in another path)
## GetPeakFileNameEx
```
string buf = reaper.GetPeakFileNameEx(string fn, string buf, boolean forWrite)
```

get the peak file name for a given file (can be either filename.reapeaks,or a hashed filename in another path)
## GetPeakFileNameEx2
```
string buf = reaper.GetPeakFileNameEx2(string fn, string buf, boolean forWrite, string peaksfileextension)
```

Like GetPeakFileNameEx, but you can specify peaksfileextension such as ".reapeaks"
## GetPlayPosition
```
number reaper.GetPlayPosition()
```

returns latency-compensated actual-what-you-hear position
## GetPlayPosition2
```
number reaper.GetPlayPosition2()
```

returns position of next audio block being processed
## GetPlayPosition2Ex
```
number reaper.GetPlayPosition2Ex(ReaProject proj)
```

returns position of next audio block being processed
## GetPlayPositionEx
```
number reaper.GetPlayPositionEx(ReaProject proj)
```

returns latency-compensated actual-what-you-hear position
## GetPlayState
```
integer reaper.GetPlayState()
```

&1=playing, &2=paused, &4=is recording
## GetPlayStateEx
```
integer reaper.GetPlayStateEx(ReaProject proj)
```

&1=playing, &2=paused, &4=is recording
## GetProjectLength
```
number reaper.GetProjectLength(ReaProject proj)
```

returns length of project (maximum of end of media item, markers, end of regions, tempo map
## GetProjectName
```
string buf = reaper.GetProjectName(ReaProject proj)
```

No description available.
## GetProjectPath
```
string buf = reaper.GetProjectPath()
```

Get the project recording path.
## GetProjectPathEx
```
string buf = reaper.GetProjectPathEx(ReaProject proj)
```

Get the project recording path.
## GetProjectStateChangeCount
```
integer reaper.GetProjectStateChangeCount(ReaProject proj)
```

returns an integer that changes when the project state changes
## GetProjectTimeOffset
```
number reaper.GetProjectTimeOffset(ReaProject proj, boolean rndframe)
```

Gets project time offset in seconds (project settings - project start time). If rndframe is true, the offset is rounded to a multiple of the project frame size.
## GetProjectTimeSignature
```
number bpm, number bpi = reaper.GetProjectTimeSignature()
```

deprecated
## GetProjectTimeSignature2
```
number bpm, number bpi = reaper.GetProjectTimeSignature2(ReaProject proj)
```

Gets basic time signature (beats per minute, numerator of time signature in bpi)
this does not reflect tempo envelopes but is purely what is set in the project settings.
## GetProjExtState
```
integer retval, string val = reaper.GetProjExtState(ReaProject proj, string extname, string key)
```

Get the value previously associated with this extname and key, the last time the project was saved. See SetProjExtState, EnumProjExtState.
## GetResourcePath
```
string reaper.GetResourcePath()
```

returns path where ini files are stored, other things are in subdirectories.
## GetSelectedEnvelope
```
TrackEnvelope reaper.GetSelectedEnvelope(ReaProject proj)
```

get the currently selected envelope, returns NULL/nil if no envelope is selected
## GetSelectedMediaItem
```
MediaItem reaper.GetSelectedMediaItem(ReaProject proj, integer selitem)
```

Discouraged, because GetSelectedMediaItem can be inefficient if media items are added, rearranged, or deleted in between calls. Instead see CountMediaItems, GetMediaItem, IsMediaItemSelected.
## GetSelectedTrack
```
MediaTrack reaper.GetSelectedTrack(ReaProject proj, integer seltrackidx)
```

Get a selected track from a project (proj=0 for active project) by selected track count (zero-based). This function ignores the master track, see GetSelectedTrack2.
## GetSelectedTrack2
```
MediaTrack reaper.GetSelectedTrack2(ReaProject proj, integer seltrackidx, boolean wantmaster)
```

Get a selected track from a project (proj=0 for active project) by selected track count (zero-based).
## GetSelectedTrackEnvelope
```
TrackEnvelope reaper.GetSelectedTrackEnvelope(ReaProject proj)
```

get the currently selected track envelope, returns NULL/nil if no envelope is selected
## GetSet_ArrangeView2
```
number start_time, number end_time = reaper.GetSet_ArrangeView2(ReaProject proj, boolean isSet, integer screen_x_start, integer screen_x_end, number start_time, number end_time)
```

Gets or sets the arrange view start/end time for screen coordinates. use screen_x_start=screen_x_end=0 to use the full arrange view's start/end time
## GetSet_LoopTimeRange
```
number start, number end = reaper.GetSet_LoopTimeRange(boolean isSet, boolean isLoop, number start, number end, boolean allowautoseek)
```

No description available.
## GetSet_LoopTimeRange2
```
number start, number end = reaper.GetSet_LoopTimeRange2(ReaProject proj, boolean isSet, boolean isLoop, number start, number end, boolean allowautoseek)
```

No description available.
## GetSetAutomationItemInfo
```
number reaper.GetSetAutomationItemInfo(TrackEnvelope env, integer autoitem_idx, string desc, number value, boolean is_set)
```

Get or set automation item information. autoitem_idx=0 for the first automation item on an envelope, 1 for the second item, etc. desc can be any of the following:
D_POOL_ID : double * : automation item pool ID (as an integer); edits are propagated to all other automation items that share a pool ID
D_POSITION : double * : automation item timeline position in seconds
D_LENGTH : double * : automation item length in seconds
D_STARTOFFS : double * : automation item start offset in seconds
D_PLAYRATE : double * : automation item playback rate
D_BASELINE : double * : automation item baseline value in the range [0,1]
D_AMPLITUDE : double * : automation item amplitude in the range [-1,1]
D_LOOPSRC : double * : nonzero if the automation item contents are looped
D_UISEL : double * : nonzero if the automation item is selected in the arrange view
D_POOL_QNLEN : double * : automation item pooled source length in quarter notes (setting will affect all pooled instances)
## GetSetAutomationItemInfo_String
```
boolean retval, string valuestrNeedBig = reaper.GetSetAutomationItemInfo_String(TrackEnvelope env, integer autoitem_idx, string desc, string valuestrNeedBig, boolean is_set)
```

Get or set automation item information. autoitem_idx=0 for the first automation item on an envelope, 1 for the second item, etc. returns true on success. desc can be any of the following:
P_POOL_NAME : char * : name of the underlying automation item pool
P_POOL_EXT:xyz : char * : extension-specific persistent data
## GetSetEnvelopeInfo_String
```
boolean retval, string stringNeedBig = reaper.GetSetEnvelopeInfo_String(TrackEnvelope env, string parmname, string stringNeedBig, boolean setNewValue)
```

Gets/sets an attribute string:
ACTIVE : active state (bool as a string "0" or "1")
ARM : armed state (bool...)
VISIBLE : visible state (bool...)
SHOWLANE : show envelope in separate lane (bool...)
GUID : (read-only) GUID as a string {xyz-....}
P_EXT:xyz : extension-specific persistent data
Note that when writing some of these attributes you will need to manually update the arrange and/or track panels, see TrackList_AdjustWindows
## GetSetEnvelopeState
```
boolean retval, string str = reaper.GetSetEnvelopeState(TrackEnvelope env, string str)
```

deprecated -- see SetEnvelopeStateChunk, GetEnvelopeStateChunk
## GetSetEnvelopeState2
```
boolean retval, string str = reaper.GetSetEnvelopeState2(TrackEnvelope env, string str, boolean isundo)
```

deprecated -- see SetEnvelopeStateChunk, GetEnvelopeStateChunk
## GetSetItemState
```
boolean retval, string str = reaper.GetSetItemState(MediaItem item, string str)
```

deprecated -- see SetItemStateChunk, GetItemStateChunk
## GetSetItemState2
```
boolean retval, string str = reaper.GetSetItemState2(MediaItem item, string str, boolean isundo)
```

deprecated -- see SetItemStateChunk, GetItemStateChunk
## GetSetMediaItemInfo_String
```
boolean retval, string stringNeedBig = reaper.GetSetMediaItemInfo_String(MediaItem item, string parmname, string stringNeedBig, boolean setNewValue)
```

Gets/sets an item attribute string:
P_NOTES : char * : item note text (do not write to returned pointer, use setNewValue to update)
P_EXT:xyz : char * : extension-specific persistent data
GUID : GUID * : 16-byte GUID, can query or update. If using a _String() function, GUID is a string {xyz-...}.
## GetSetMediaItemTakeInfo_String
```
boolean retval, string stringNeedBig = reaper.GetSetMediaItemTakeInfo_String(MediaItem_Take tk, string parmname, string stringNeedBig, boolean setNewValue)
```

Gets/sets a take attribute string:
P_NAME : char * : take name
P_EXT:xyz : char * : extension-specific persistent data
GUID : GUID * : 16-byte GUID, can query or update. If using a _String() function, GUID is a string {xyz-...}.
## GetSetMediaTrackInfo_String
```
boolean retval, string stringNeedBig = reaper.GetSetMediaTrackInfo_String(MediaTrack tr, string parmname, string stringNeedBig, boolean setNewValue)
```

Get or set track string attributes.
P_NAME : char * : track name (on master returns NULL)
P_ICON : const char * : track icon (full filename, or relative to resource_path/data/track_icons)
P_LANENAME:n : char * : lane name (returns NULL for non-fixed-lane-tracks)
P_MCP_LAYOUT : const char * : layout name
P_RAZOREDITS : const char * : list of razor edit areas, as space-separated triples of start time, end time, and envelope GUID string. Example: "0.0 1.0 \"\" 0.0 1.0 "{xyz-...}"
P_RAZOREDITS_EXT : const char * : list of razor edit areas, as comma-separated sets of space-separated tuples of start time, end time, optional: envelope GUID string, fixed/fipm top y-position, fixed/fipm bottom y-position. Example: "0.0 1.0,0.0 1.0 "{xyz-...}",1.0 2.0 "" 0.25 0.75"
P_TCP_LAYOUT : const char * : layout name
P_EXT:xyz : char * : extension-specific persistent data
P_UI_RECT:tcp.mute : char * : read-only, allows querying screen position + size of track WALTER elements (tcp.size queries screen position and size of entire TCP, etc).
GUID : GUID * : 16-byte GUID, can query or update. If using a _String() function, GUID is a string {xyz-...}.
## GetSetProjectAuthor
```
string author = reaper.GetSetProjectAuthor(ReaProject proj, boolean set, string author)
```

deprecated, see GetSetProjectInfo_String with desc="PROJECT_AUTHOR"
## GetSetProjectGrid
```
integer retval, optional number division, optional integer swingmode, optional number swingamt = reaper.GetSetProjectGrid(ReaProject project, boolean set, optional number division, optional integer swingmode, optional number swingamt)
```

Get or set the arrange view grid division. 0.25=quarter note, 1.0/3.0=half note triplet, etc. swingmode can be 1 for swing enabled, swingamt is -1..1. swingmode can be 3 for measure-grid. Returns grid configuration flags
## GetSetProjectInfo
```
number reaper.GetSetProjectInfo(ReaProject project, string desc, number value, boolean is_set)
```

Get or set project information.
RENDER_SETTINGS : &(1|2)=0:master mix, &1=stems+master mix, &2=stems only, &4=multichannel tracks to multichannel files, &8=use render matrix, &16=tracks with only mono media to mono files, &32=selected media items, &64=selected media items via master, &128=selected tracks via master, &256=embed transients if format supports, &512=embed metadata if format supports, &1024=embed take markers if format supports, &2048=2nd pass render
RENDER_BOUNDSFLAG : 0=custom time bounds, 1=entire project, 2=time selection, 3=all project regions, 4=selected media items, 5=selected project regions, 6=all project markers, 7=selected project markers
RENDER_CHANNELS : number of channels in rendered file
RENDER_SRATE : sample rate of rendered file (or 0 for project sample rate)
RENDER_STARTPOS : render start time when RENDER_BOUNDSFLAG=0
RENDER_ENDPOS : render end time when RENDER_BOUNDSFLAG=0
RENDER_TAILFLAG : apply render tail setting when rendering: &1=custom time bounds, &2=entire project, &4=time selection, &8=all project markers/regions, &16=selected media items, &32=selected project markers/regions
RENDER_TAILMS : tail length in ms to render (only used if RENDER_BOUNDSFLAG and RENDER_TAILFLAG are set)
RENDER_ADDTOPROJ : &1=add rendered files to project, &2=do not render files that are likely silent
RENDER_DITHER : &1=dither, &2=noise shaping, &4=dither stems, &8=noise shaping on stems
RENDER_NORMALIZE: &1=enable, (&14==0)=LUFS-I, (&14==2)=RMS, (&14==4)=peak, (&14==6)=true peak, (&14==8)=LUFS-M max, (&14==10)=LUFS-S max, &64=enable brickwall limit, &128=brickwall limit true peak, (&(256|2048)==256)=only normalize files that are too loud, (&(256|2048)==2048)=only normalize files that are too quiet, &512=apply fade-in, &1024=apply fade-out, (&(32|4096)==32)=normalize stems as if files play together (common gain), (&(32|4096)==4096)=normalize to loudest file, (&(32|4096)==4128)=normalize as if files play together, &8192=adjust mono media additional -3dB, &(1<<16)=pad start with silence, &(2<<16)=pad end with silence, &(4<<16)=disable all render postprocessing, &(32<<16)=limit as if files play together
RENDER_NORMALIZE_TARGET: render normalization target (0.5 means -6.02dB, requires RENDER_NORMALIZE&1)
RENDER_BRICKWALL: render brickwall limit (0.5 means -6.02dB, requires RENDER_NORMALIZE&64)
RENDER_FADEIN: render fade-in (0.001 means 1 ms, requires RENDER_NORMALIZE&512)
RENDER_FADEOUT: render fade-out (0.001 means 1 ms, requires RENDER_NORMALIZE&1024)
RENDER_FADEINSHAPE: render fade-in shape
RENDER_FADEOUTSHAPE: render fade-out shape
RENDER_PADSTART: pad render start with silence (0.001 means 1ms, requires RENDER_NORMALIZE&(1<<16))RENDER_PADEND: pad render end with silence (0.001 means 1ms, requires RENDER_NORMALIZE&(2<<16))PROJECT_SRATE : sample rate (ignored unless PROJECT_SRATE_USE set)
PROJECT_SRATE_USE : set to 1 if project sample rate is used
## GetSetProjectInfo_String
```
boolean retval, string valuestrNeedBig = reaper.GetSetProjectInfo_String(ReaProject project, string desc, string valuestrNeedBig, boolean is_set)
```

Get or set project information.
PROJECT_NAME : project file name (read-only, is_set will be ignored)
PROJECT_TITLE : title field from Project Settings/Notes dialog
PROJECT_AUTHOR : author field from Project Settings/Notes dialog
TRACK_GROUP_NAME:X : track group name, X should be 1..64
MARKER_GUID:X : get the GUID (unique ID) of the marker or region with index X, where X is the index passed to EnumProjectMarkers, not necessarily the displayed number (read-only)
MARKER_INDEX_FROM_GUID:{GUID} : get the GUID index of the marker or region with GUID {GUID} (read-only)
OPENCOPY_CFGIDX : integer for the configuration of format to use when creating copies/applying FX. 0=wave (auto-depth), 1=APPLYFX_FORMAT, 2=RECORD_FORMAT
RECORD_PATH : recording directory -- may be blank or a relative path, to get the effective path see GetProjectPathEx()
RECORD_PATH_SECONDARY : secondary recording directory
RECORD_FORMAT : base64-encoded sink configuration (see project files, etc). Callers can also pass a simple 4-byte string (non-base64-encoded), e.g. "evaw" or "l3pm", to use default settings for that sink type.
APPLYFX_FORMAT : base64-encoded sink configuration (see project files, etc). Used only if RECFMT_OPENCOPY is set to 1. Callers can also pass a simple 4-byte string (non-base64-encoded), e.g. "evaw" or "l3pm", to use default settings for that sink type.
RECTAG : project recording tag wildcard ($rectag). Can be used in Preferences/Audio/Recording to auto-name recorded files.
RENDER_FILE : render directory
RENDER_PATTERN : render file name (may contain wildcards)
RENDER_METADATA : get or set the metadata saved with the project (not metadata embedded in project media). Example, ID3 album name metadata: valuestr="ID3:TALB" to get, valuestr="ID3:TALB|my album name" to set. Call with valuestr="" and is_set=false to get a semicolon-separated list of defined project metadata identifiers.
RENDER_TARGETS : semicolon separated list of files that would be written if the project is rendered using the most recent render settings
RENDER_STATS : (read-only) semicolon separated list of statistics for the most recently rendered files. call with valuestr="XXX" to run an action (for example, "42437"=dry run render selected items) before returning statistics.
RENDER_FORMAT : base64-encoded sink configuration (see project files, etc). Callers can also pass a simple 4-byte string (non-base64-encoded), e.g. "evaw" or "l3pm", to use default settings for that sink type.
RENDER_FORMAT2 : base64-encoded secondary sink configuration. Callers can also pass a simple 4-byte string (non-base64-encoded), e.g. "evaw" or "l3pm", to use default settings for that sink type, or "" to disable secondary render. Formats available on this machine: "wave" "aiff" "caff" "raw " "iso " "ddp " "flac" "mp3l" "oggv" "OggS" "FFMP" "WMF " "GIF " "LCF " "wvpk"
## GetSetProjectNotes
```
string notes = reaper.GetSetProjectNotes(ReaProject proj, boolean set, string notes)
```

gets or sets project notes, notesNeedBig_sz is ignored when setting
## GetSetRepeat
```
integer reaper.GetSetRepeat(integer val)
```

-1 == query,0=clear,1=set,>1=toggle . returns new value
## GetSetRepeatEx
```
integer reaper.GetSetRepeatEx(ReaProject proj, integer val)
```

-1 == query,0=clear,1=set,>1=toggle . returns new value
## GetSetTempoTimeSigMarkerFlag
```
integer reaper.GetSetTempoTimeSigMarkerFlag(ReaProject project, integer point_index, integer flag, boolean is_set)
```

Gets or sets the attribute flag of a tempo/time signature marker. flag &1=sets time signature and starts new measure, &2=does not set tempo, &4=allow previous partial measure if starting new measure, &8=set new metronome pattern if starting new measure, &16=reset ruler grid if starting new measure
## GetSetTrackGroupMembership
```
integer reaper.GetSetTrackGroupMembership(MediaTrack tr, string groupname, integer setmask, integer setvalue)
```

Gets or modifies the group membership for a track. Returns group state prior to call (each bit represents one of the 32 group numbers). if setmask has bits set, those bits in setvalue will be applied to group. Group can be one of:
MEDIA_EDIT_LEAD
MEDIA_EDIT_FOLLOW
VOLUME_LEAD
VOLUME_FOLLOW
VOLUME_VCA_LEAD
VOLUME_VCA_FOLLOW
PAN_LEAD
PAN_FOLLOW
WIDTH_LEAD
WIDTH_FOLLOW
MUTE_LEAD
MUTE_FOLLOW
SOLO_LEAD
SOLO_FOLLOW
RECARM_LEAD
RECARM_FOLLOW
POLARITY_LEAD
POLARITY_FOLLOW
AUTOMODE_LEAD
AUTOMODE_FOLLOW
VOLUME_REVERSE
PAN_REVERSE
WIDTH_REVERSE
NO_LEAD_WHEN_FOLLOW
VOLUME_VCA_FOLLOW_ISPREFX
## GetSetTrackGroupMembershipEx
```
integer reaper.GetSetTrackGroupMembershipEx(MediaTrack tr, string groupname, integer offset, integer setmask, integer setvalue)
```

Gets or modifies 32 bits (at offset, where 0 is the low 32 bits of the grouping) of the group membership for a track. Returns group state prior to call. if setmask has bits set, those bits in setvalue will be applied to group. Group can be one of:
MEDIA_EDIT_LEAD
MEDIA_EDIT_FOLLOW
VOLUME_LEAD
VOLUME_FOLLOW
VOLUME_VCA_LEAD
VOLUME_VCA_FOLLOW
PAN_LEAD
PAN_FOLLOW
WIDTH_LEAD
WIDTH_FOLLOW
MUTE_LEAD
MUTE_FOLLOW
SOLO_LEAD
SOLO_FOLLOW
RECARM_LEAD
RECARM_FOLLOW
POLARITY_LEAD
POLARITY_FOLLOW
AUTOMODE_LEAD
AUTOMODE_FOLLOW
VOLUME_REVERSE
PAN_REVERSE
WIDTH_REVERSE
NO_LEAD_WHEN_FOLLOW
VOLUME_VCA_FOLLOW_ISPREFX
## GetSetTrackGroupMembershipHigh
```
integer reaper.GetSetTrackGroupMembershipHigh(MediaTrack tr, string groupname, integer setmask, integer setvalue)
```

Gets or modifies the group membership for a track. Returns group state prior to call (each bit represents one of the high 32 group numbers). if setmask has bits set, those bits in setvalue will be applied to group. Group can be one of:
MEDIA_EDIT_LEAD
MEDIA_EDIT_FOLLOW
VOLUME_LEAD
VOLUME_FOLLOW
VOLUME_VCA_LEAD
VOLUME_VCA_FOLLOW
PAN_LEAD
PAN_FOLLOW
WIDTH_LEAD
WIDTH_FOLLOW
MUTE_LEAD
MUTE_FOLLOW
SOLO_LEAD
SOLO_FOLLOW
RECARM_LEAD
RECARM_FOLLOW
POLARITY_LEAD
POLARITY_FOLLOW
AUTOMODE_LEAD
AUTOMODE_FOLLOW
VOLUME_REVERSE
PAN_REVERSE
WIDTH_REVERSE
NO_LEAD_WHEN_FOLLOW
VOLUME_VCA_FOLLOW_ISPREFX
## GetSetTrackSendInfo_String
```
boolean retval, string stringNeedBig = reaper.GetSetTrackSendInfo_String(MediaTrack tr, integer category, integer sendidx, string parmname, string stringNeedBig, boolean setNewValue)
```

Gets/sets a send attribute string:
P_EXT:xyz : char * : extension-specific persistent data
## GetSetTrackState
```
boolean retval, string str = reaper.GetSetTrackState(MediaTrack track, string str)
```

deprecated -- see SetTrackStateChunk, GetTrackStateChunk
## GetSetTrackState2
```
boolean retval, string str = reaper.GetSetTrackState2(MediaTrack track, string str, boolean isundo)
```

deprecated -- see SetTrackStateChunk, GetTrackStateChunk
## GetSubProjectFromSource
```
ReaProject reaper.GetSubProjectFromSource(PCM_source src)
```

No description available.
## GetTake
```
MediaItem_Take reaper.GetTake(MediaItem item, integer takeidx)
```

get a take from an item by take count (zero-based)
## GetTakeEnvelope
```
TrackEnvelope reaper.GetTakeEnvelope(MediaItem_Take take, integer envidx)
```

No description available.
## GetTakeEnvelopeByName
```
TrackEnvelope reaper.GetTakeEnvelopeByName(MediaItem_Take take, string envname)
```

No description available.
## GetTakeMarker
```
number retval, string name, optional integer color = reaper.GetTakeMarker(MediaItem_Take take, integer idx)
```

Get information about a take marker. Returns the position in media item source time, or -1 if the take marker does not exist. See GetNumTakeMarkers, SetTakeMarker, DeleteTakeMarker
## GetTakeName
```
string reaper.GetTakeName(MediaItem_Take take)
```

returns NULL if the take is not valid
## GetTakeNumStretchMarkers
```
integer reaper.GetTakeNumStretchMarkers(MediaItem_Take take)
```

Returns number of stretch markers in take
## GetTakeStretchMarker
```
integer retval, number pos, optional number srcpos = reaper.GetTakeStretchMarker(MediaItem_Take take, integer idx)
```

Gets information on a stretch marker, idx is 0..n. Returns -1 if stretch marker not valid. posOut will be set to position in item, srcposOutOptional will be set to source media position. Returns index. if input index is -1, the following marker is found using position (or source position if position is -1). If position/source position are used to find marker position, their values are not updated.
## GetTakeStretchMarkerSlope
```
number reaper.GetTakeStretchMarkerSlope(MediaItem_Take take, integer idx)
```

See SetTakeStretchMarkerSlope
## GetTCPFXParm
```
boolean retval, integer fxindex, integer parmidx = reaper.GetTCPFXParm(ReaProject project, MediaTrack track, integer index)
```

Get information about a specific FX parameter knob (see CountTCPFXParms).
## GetTempoMatchPlayRate
```
boolean retval, number rate, number targetlen = reaper.GetTempoMatchPlayRate(PCM_source source, number srcscale, number position, number mult)
```

finds the playrate and target length to insert this item stretched to a round power-of-2 number of bars, between 1/8 and 256
## GetTempoTimeSigMarker
```
boolean retval, number timepos, integer measurepos, number beatpos, number bpm, integer timesig_num, integer timesig_denom, boolean lineartempo = reaper.GetTempoTimeSigMarker(ReaProject proj, integer ptidx)
```

Get information about a tempo/time signature marker. See CountTempoTimeSigMarkers, SetTempoTimeSigMarker, AddTempoTimeSigMarker.
## GetThemeColor
```
integer reaper.GetThemeColor(string ini_key, integer flags)
```

Returns the theme color specified, or -1 on failure. If the low bit of flags is set, the color as originally specified by the theme (before any transformations) is returned, otherwise the current (possibly transformed and modified) color is returned. See SetThemeColor for a list of valid ini_key.
## GetThingFromPoint
```
MediaTrack retval, string info = reaper.GetThingFromPoint(integer screen_x, integer screen_y)
```

Hit tests a point in screen coordinates. Updates infoOut with information such as "arrange", "fx_chain", "fx_0" (first FX in chain, floating), "spacer_0" (spacer before first track). If a track panel is hit, string will begin with "tcp" or "mcp" or "tcp.mute" etc (future versions may append additional information). May return NULL with valid info string to indicate non-track thing.
## GetToggleCommandState
```
integer reaper.GetToggleCommandState(integer command_id)
```

See GetToggleCommandStateEx.
## GetToggleCommandStateEx
```
integer reaper.GetToggleCommandStateEx(integer section_id, integer command_id)
```

For the main action context, the MIDI editor, or the media explorer, returns the toggle state of the action. 0=off, 1=on, -1=NA because the action does not have on/off states. For the MIDI editor, the action state for the most recently focused window will be returned.
## GetTooltipWindow
```
HWND reaper.GetTooltipWindow()
```

gets a tooltip window,in case you want to ask it for font information. Can return NULL.
## GetTouchedOrFocusedFX
```
boolean retval, integer trackidx, integer itemidx, integer takeidx, integer fxidx, integer parm = reaper.GetTouchedOrFocusedFX(integer mode)
```

mode can be 0 to query last touched parameter, or 1 to query currently focused FX. Returns false if failed. If successful, trackIdxOut will be track index (-1 is master track, 0 is first track). itemidxOut will be 0-based item index if an item, or -1 if not an item. takeidxOut will be 0-based take index. fxidxOut will be FX index, potentially with 0x2000000 set to signify container-addressing, or with 0x1000000 set to signify record-input FX. parmOut will be set to the parameter index if querying last-touched. parmOut will have 1 set if querying focused state and FX is no longer focused but still open.
## GetTrack
```
MediaTrack reaper.GetTrack(ReaProject proj, integer trackidx)
```

get a track from a project by track count (zero-based) (proj=0 for active project)
## GetTrackAutomationMode
```
integer reaper.GetTrackAutomationMode(MediaTrack tr)
```

return the track mode, regardless of global override
## GetTrackColor
```
integer reaper.GetTrackColor(MediaTrack track)
```

Returns the track custom color as OS dependent color|0x1000000 (i.e. ColorToNative(r,g,b)|0x1000000). Black is returned as 0x1000000, no color setting is returned as 0.
## GetTrackDepth
```
integer reaper.GetTrackDepth(MediaTrack track)
```

No description available.
## GetTrackEnvelope
```
TrackEnvelope reaper.GetTrackEnvelope(MediaTrack track, integer envidx)
```

No description available.
## GetTrackEnvelopeByChunkName
```
TrackEnvelope reaper.GetTrackEnvelopeByChunkName(MediaTrack tr, string cfgchunkname_or_guid)
```

Gets a built-in track envelope by configuration chunk name, like "<VOLENV", or GUID string, like "{B577250D-146F-B544-9B34-F24FBE488F1F}".
## GetTrackEnvelopeByName
```
TrackEnvelope reaper.GetTrackEnvelopeByName(MediaTrack track, string envname)
```

No description available.
## GetTrackFromPoint
```
MediaTrack retval, optional integer info = reaper.GetTrackFromPoint(integer screen_x, integer screen_y)
```

Returns the track from the screen coordinates specified. If the screen coordinates refer to a window associated to the track (such as FX), the track will be returned. infoOutOptional will be set to 1 if it is likely an envelope, 2 if it is likely a track FX. For a free item positioning or fixed lane track, the second byte of infoOutOptional will be set to the (approximate, for fipm tracks) item lane underneath the mouse. See GetThingFromPoint.
## GetTrackGUID
```
string GUID = reaper.GetTrackGUID(MediaTrack tr)
```

No description available.
## GetTrackMediaItem
```
MediaItem reaper.GetTrackMediaItem(MediaTrack tr, integer itemidx)
```

No description available.
## GetTrackMIDILyrics
```
boolean retval, string buf = reaper.GetTrackMIDILyrics(MediaTrack track, integer flag)
```

Get all MIDI lyrics on the track. Lyrics will be returned as one string with tabs between each word. flag&1: double tabs at the end of each measure and triple tabs when skipping measures, flag&2: each lyric is preceded by its beat position in the project (example with flag=2: "1.1.2\tLyric for measure 1 beat 2\t2.1.1\tLyric for measure 2 beat 1	"). See SetTrackMIDILyrics
## GetTrackMIDINoteName
```
string reaper.GetTrackMIDINoteName(integer track, integer pitch, integer chan)
```

see GetTrackMIDINoteNameEx
## GetTrackMIDINoteNameEx
```
string reaper.GetTrackMIDINoteNameEx(ReaProject proj, MediaTrack track, integer pitch, integer chan)
```

Get note/CC name. pitch 128 for CC0 name, 129 for CC1 name, etc. See SetTrackMIDINoteNameEx
## GetTrackMIDINoteRange
```
integer note_lo, integer note_hi = reaper.GetTrackMIDINoteRange(ReaProject proj, MediaTrack track)
```

No description available.
## GetTrackName
```
boolean retval, string buf = reaper.GetTrackName(MediaTrack track)
```

Returns "MASTER" for master track, "Track N" if track has no name.
## GetTrackNumMediaItems
```
integer reaper.GetTrackNumMediaItems(MediaTrack tr)
```

No description available.
## GetTrackNumSends
```
integer reaper.GetTrackNumSends(MediaTrack tr, integer category)
```

returns number of sends/receives/hardware outputs - category is <0 for receives, 0=sends, >0 for hardware outputs
## GetTrackReceiveName
```
boolean retval, string buf = reaper.GetTrackReceiveName(MediaTrack track, integer recv_index)
```

See GetTrackSendName.
## GetTrackReceiveUIMute
```
boolean retval, boolean mute = reaper.GetTrackReceiveUIMute(MediaTrack track, integer recv_index)
```

See GetTrackSendUIMute.
## GetTrackReceiveUIVolPan
```
boolean retval, number volume, number pan = reaper.GetTrackReceiveUIVolPan(MediaTrack track, integer recv_index)
```

See GetTrackSendUIVolPan.
## GetTrackSendInfo_Value
```
number reaper.GetTrackSendInfo_Value(MediaTrack tr, integer category, integer sendidx, string parmname)
```

Get send/receive/hardware output numerical-value attributes.
category is <0 for receives, 0=sends, >0 for hardware outputs
parameter names:
B_MUTE : bool *
B_PHASE : bool * : true to flip phase
B_MONO : bool *
D_VOL : double * : 1.0 = +0dB etc
D_PAN : double * : -1..+1
D_PANLAW : double * : 1.0=+0.0db, 0.5=-6dB, -1.0 = projdef etc
I_SENDMODE : int * : 0=post-fader, 1=pre-fx, 2=post-fx (deprecated), 3=post-fx
I_AUTOMODE : int * : automation mode (-1=use track automode, 0=trim/off, 1=read, 2=touch, 3=write, 4=latch)
I_SRCCHAN : int * : -1 for no audio send. Low 10 bits specify channel offset, and higher bits specify channel count. (srcchan>>10) == 0 for stereo, 1 for mono, 2 for 4 channel, 3 for 6 channel, etc.
I_DSTCHAN : int * : low 10 bits are destination index, &1024 set to mix to mono.
I_MIDIFLAGS : int * : low 5 bits=source channel 0=all, 1-16, 31=MIDI send disabled, next 5 bits=dest channel, 0=orig, 1-16=chan. &1024 for faders-send MIDI vol/pan. (>>14)&255 = src bus (0 for all, 1 for normal, 2+). (>>22)&255=destination bus (0 for all, 1 for normal, 2+)
P_DESTTRACK : MediaTrack * : destination track, only applies for sends/recvs (read-only)
P_SRCTRACK : MediaTrack * : source track, only applies for sends/recvs (read-only)
P_ENV:<envchunkname : TrackEnvelope * : call with :<VOLENV, :<PANENV, etc appended (read-only)
See CreateTrackSend, RemoveTrackSend, GetTrackNumSends.
## GetTrackSendName
```
boolean retval, string buf = reaper.GetTrackSendName(MediaTrack track, integer send_index)
```

send_idx>=0 for hw ouputs, >=nb_of_hw_ouputs for sends. See GetTrackReceiveName.
## GetTrackSendUIMute
```
boolean retval, boolean mute = reaper.GetTrackSendUIMute(MediaTrack track, integer send_index)
```

send_idx>=0 for hw ouputs, >=nb_of_hw_ouputs for sends. See GetTrackReceiveUIMute.
## GetTrackSendUIVolPan
```
boolean retval, number volume, number pan = reaper.GetTrackSendUIVolPan(MediaTrack track, integer send_index)
```

send_idx>=0 for hw ouputs, >=nb_of_hw_ouputs for sends. See GetTrackReceiveUIVolPan.
## GetTrackState
```
string retval, integer flags = reaper.GetTrackState(MediaTrack track)
```

Gets track state, returns track name.
flags will be set to:
&1=folder
&2=selected
&4=has fx enabled
&8=muted
&16=soloed
&32=SIP'd (with &16)
&64=rec armed
&128=rec monitoring on
&256=rec monitoring auto
&512=hide from TCP
&1024=hide from MCP
## GetTrackStateChunk
```
boolean retval, string str = reaper.GetTrackStateChunk(MediaTrack track, string str, boolean isundo)
```

Gets the RPPXML state of a track, returns true if successful. Undo flag is a performance/caching hint.
## GetTrackUIMute
```
boolean retval, boolean mute = reaper.GetTrackUIMute(MediaTrack track)
```

No description available.
## GetTrackUIPan
```
boolean retval, number pan1, number pan2, integer panmode = reaper.GetTrackUIPan(MediaTrack track)
```

No description available.
## GetTrackUIVolPan
```
boolean retval, number volume, number pan = reaper.GetTrackUIVolPan(MediaTrack track)
```

No description available.
## GetUnderrunTime
```
integer audio_xrun, integer media_xrun, integer curtime = reaper.GetUnderrunTime()
```

retrieves the last timestamps of audio xrun (yellow-flash, if available), media xrun (red-flash), and the current time stamp (all milliseconds)
## GetUserFileNameForRead
```
boolean retval, string filenameNeed4096 = reaper.GetUserFileNameForRead(string filenameNeed4096, string title, string defext)
```

returns true if the user selected a valid file, false if the user canceled the dialog
## GetUserInputs
```
boolean retval, string retvals_csv = reaper.GetUserInputs(string title, integer num_inputs, string captions_csv, string retvals_csv)
```

Get values from the user.
If a caption begins with *, for example "*password", the edit field will not display the input text.
Maximum fields is 16. Values are returned as a comma-separated string. Returns false if the user canceled the dialog. You can supply special extra information via additional caption fields: extrawidth=XXX to increase text field width, separator=X to use a different separator for returned fields.
## GoToMarker
```
reaper.GoToMarker(ReaProject proj, integer marker_index, boolean use_timeline_order)
```

Go to marker. If use_timeline_order==true, marker_index 1 refers to the first marker on the timeline. If use_timeline_order==false, marker_index 1 refers to the first marker with the user-editable index of 1.
## GoToRegion
```
reaper.GoToRegion(ReaProject proj, integer region_index, boolean use_timeline_order)
```

Seek to region after current region finishes playing (smooth seek). If use_timeline_order==true, region_index 1 refers to the first region on the timeline. If use_timeline_order==false, region_index 1 refers to the first region with the user-editable index of 1.
## GR_SelectColor
```
integer retval, integer color = reaper.GR_SelectColor(HWND hwnd)
```

Runs the system color chooser dialog. Returns 0 if the user cancels the dialog.
## GSC_mainwnd
```
integer reaper.GSC_mainwnd(integer t)
```

this is just like win32 GetSysColor() but can have overrides.
## guidToString
```
string destNeed64 = reaper.guidToString(string gGUID, string destNeed64)
```

dest should be at least 64 chars long to be safe
## HasExtState
```
boolean reaper.HasExtState(string section, string key)
```

Returns true if there exists an extended state value for a specific section and key. See SetExtState, GetExtState, DeleteExtState.
## HasTrackMIDIPrograms
```
string reaper.HasTrackMIDIPrograms(integer track)
```

returns name of track plugin that is supplying MIDI programs,or NULL if there is none
## HasTrackMIDIProgramsEx
```
string reaper.HasTrackMIDIProgramsEx(ReaProject proj, MediaTrack track)
```

returns name of track plugin that is supplying MIDI programs,or NULL if there is none
## Help_Set
```
reaper.Help_Set(string helpstring, boolean is_temporary_help)
```

No description available.
## image_resolve_fn
```
string out = reaper.image_resolve_fn(string in, string out)
```

No description available.
## InsertAutomationItem
```
integer reaper.InsertAutomationItem(TrackEnvelope env, integer pool_id, number position, number length)
```

Insert a new automation item. pool_id < 0 collects existing envelope points into the automation item; if pool_id is >= 0 the automation item will be a new instance of that pool (which will be created as an empty instance if it does not exist). Returns the index of the item, suitable for passing to other automation item API functions. See GetSetAutomationItemInfo.
## InsertEnvelopePoint
```
boolean reaper.InsertEnvelopePoint(TrackEnvelope envelope, number time, number value, integer shape, number tension, boolean selected, optional boolean noSortIn)
```

Insert an envelope point. If setting multiple points at once, set noSort=true, and call Envelope_SortPoints when done. See InsertEnvelopePointEx.
## InsertEnvelopePointEx
```
boolean reaper.InsertEnvelopePointEx(TrackEnvelope envelope, integer autoitem_idx, number time, number value, integer shape, number tension, boolean selected, optional boolean noSortIn)
```

Insert an envelope point. If setting multiple points at once, set noSort=true, and call Envelope_SortPoints when done.
autoitem_idx=-1 for the underlying envelope, 0 for the first automation item on the envelope, etc.
For automation items, pass autoitem_idx|0x10000000 to base ptidx on the number of points in one full loop iteration,
even if the automation item is trimmed so that not all points are visible.
Otherwise, ptidx will be based on the number of visible points in the automation item, including all loop iterations.
See CountEnvelopePointsEx, GetEnvelopePointEx, SetEnvelopePointEx, DeleteEnvelopePointEx.
## InsertMedia
```
integer reaper.InsertMedia(string file, integer mode)
```

mode: 0=add to current track, 1=add new track, 3=add to selected items as takes, &4=stretch/loop to fit time sel, &8=try to match tempo 1x, &16=try to match tempo 0.5x, &32=try to match tempo 2x, &64=don't preserve pitch when matching tempo, &128=no loop/section if startpct/endpct set, &256=force loop regardless of global preference for looping imported items, &512=use high word as absolute track index if mode&3==0 or mode&2048, &1024=insert into reasamplomatic on a new track (add 1 to insert on last selected track), &2048=insert into open reasamplomatic instance (add 512 to use high word as absolute track index), &4096=move to source preferred position (BWF start offset), &8192=reverse. &16384=apply ripple according to project setting
## InsertMediaSection
```
integer reaper.InsertMediaSection(string file, integer mode, number startpct, number endpct, number pitchshift)
```

See InsertMedia.
## InsertTrackAtIndex
```
reaper.InsertTrackAtIndex(integer idx, boolean wantDefaults)
```

inserts a track at idx,of course this will be clamped to 0..GetNumTracks(). wantDefaults=TRUE for default envelopes/FX,otherwise no enabled fx/env. Superseded, see InsertTrackInProject
## InsertTrackInProject
```
reaper.InsertTrackInProject(ReaProject proj, integer idx, integer flags)
```

inserts a track in project proj at idx, this will be clamped to 0..CountTracks(proj). flags&1 for default envelopes/FX, otherwise no enabled fx/envelopes will be added.
## IsMediaExtension
```
boolean reaper.IsMediaExtension(string ext, boolean wantOthers)
```

Tests a file extension (i.e. "wav" or "mid") to see if it's a media extension.
If wantOthers is set, then "RPP", "TXT" and other project-type formats will also pass.
## IsMediaItemSelected
```
boolean reaper.IsMediaItemSelected(MediaItem item)
```

No description available.
## IsProjectDirty
```
integer reaper.IsProjectDirty(ReaProject proj)
```

Is the project dirty (needing save)? Always returns 0 if 'undo/prompt to save' is disabled in preferences.
## IsTrackSelected
```
boolean reaper.IsTrackSelected(MediaTrack track)
```

No description available.
## IsTrackVisible
```
boolean reaper.IsTrackVisible(MediaTrack track, boolean mixer)
```

If mixer==true, returns true if the track is visible in the mixer. If mixer==false, returns true if the track is visible in the track control panel.
## joystick_create
```
joystick_device reaper.joystick_create(string guidGUID)
```

creates a joystick device
## joystick_destroy
```
reaper.joystick_destroy(joystick_device device)
```

destroys a joystick device
## joystick_enum
```
string retval, optional string namestr = reaper.joystick_enum(integer index)
```

enumerates installed devices, returns GUID as a string
## joystick_getaxis
```
number reaper.joystick_getaxis(joystick_device dev, integer axis)
```

returns axis value (-1..1)
## joystick_getbuttonmask
```
integer reaper.joystick_getbuttonmask(joystick_device dev)
```

returns button pressed mask, 1=first button, 2=second...
## joystick_getinfo
```
integer retval, optional integer axes, optional integer povs = reaper.joystick_getinfo(joystick_device dev)
```

returns button count
## joystick_getpov
```
number reaper.joystick_getpov(joystick_device dev, integer pov)
```

returns POV value (usually 0..655.35, or 655.35 on error)
## joystick_update
```
boolean reaper.joystick_update(joystick_device dev)
```

Updates joystick state from hardware, returns true if successful (joystick_get* will not be valid until joystick_update() is called successfully)
## kbd_enumerateActions
```
integer retval, string name = reaper.kbd_enumerateActions(KbdSectionInfo section, integer idx)
```

No description available.
## kbd_getTextFromCmd
```
string reaper.kbd_getTextFromCmd(integer cmd, KbdSectionInfo section)
```

No description available.
## LICE_ClipLine
```
boolean retval, integer pX1, integer pY1, integer pX2, integer pY2 = reaper.LICE_ClipLine(integer pX1, integer pY1, integer pX2, integer pY2, integer xLo, integer yLo, integer xHi, integer yHi)
```

Returns false if the line is entirely offscreen.
## LocalizeString
```
string reaper.LocalizeString(string src_string, string section, integer flags)
```

Returns a localized version of src_string, in section section. flags can have 1 set to only localize if sprintf-style formatting matches the original.
## Loop_OnArrow
```
boolean reaper.Loop_OnArrow(ReaProject project, integer direction)
```

Move the loop selection left or right. Returns true if snap is enabled.
## Main_OnCommand
```
reaper.Main_OnCommand(integer command, integer flag)
```

See Main_OnCommandEx.
## Main_OnCommandEx
```
reaper.Main_OnCommandEx(integer command, integer flag, ReaProject proj)
```

Performs an action belonging to the main action section. To perform non-native actions (ReaScripts, custom or extension plugins' actions) safely, see NamedCommandLookup().
## Main_openProject
```
reaper.Main_openProject(string name)
```

opens a project. will prompt the user to save unless name is prefixed with 'noprompt:'. If name is prefixed with 'template:', project file will be loaded as a template.
If passed a .RTrackTemplate file, adds the template to the existing project.
## Main_SaveProject
```
reaper.Main_SaveProject(ReaProject proj, boolean forceSaveAsIn)
```

Save the project.
## Main_SaveProjectEx
```
reaper.Main_SaveProjectEx(ReaProject proj, string filename, integer options)
```

Save the project. options: &1=save selected tracks as track template, &2=include media with track template, &4=include envelopes with track template, &8=if not saving template, set as the new project filename for this ReaProject. See Main_openProject, Main_SaveProject.
## Main_UpdateLoopInfo
```
reaper.Main_UpdateLoopInfo(integer ignoremask)
```

No description available.
## MarkProjectDirty
```
reaper.MarkProjectDirty(ReaProject proj)
```

Marks project as dirty (needing save) if 'undo/prompt to save' is enabled in preferences.
## MarkTrackItemsDirty
```
reaper.MarkTrackItemsDirty(MediaTrack track, MediaItem item)
```

If track is supplied, item is ignored
## Master_GetPlayRate
```
number reaper.Master_GetPlayRate(ReaProject project)
```

No description available.
## Master_GetPlayRateAtTime
```
number reaper.Master_GetPlayRateAtTime(number time_s, ReaProject proj)
```

No description available.
## Master_GetTempo
```
number reaper.Master_GetTempo()
```

No description available.
## Master_NormalizePlayRate
```
number reaper.Master_NormalizePlayRate(number playrate, boolean isnormalized)
```

Convert play rate to/from a value between 0 and 1, representing the position on the project playrate slider.
## Master_NormalizeTempo
```
number reaper.Master_NormalizeTempo(number bpm, boolean isnormalized)
```

Convert the tempo to/from a value between 0 and 1, representing bpm in the range of 40-296 bpm.
## MB
```
integer reaper.MB(string msg, string title, integer type)
```

type 0=OK,1=OKCANCEL,2=ABORTRETRYIGNORE,3=YESNOCANCEL,4=YESNO,5=RETRYCANCEL : ret 1=OK,2=CANCEL,3=ABORT,4=RETRY,5=IGNORE,6=YES,7=NO
## MediaExplorerGetLastPlayedFileInfo
```
boolean retval, string filename, integer filemode, number selstart, number selend, number pitchshift, number voladj, number rateadj, number sourcebpm, string extrainfo = reaper.MediaExplorerGetLastPlayedFileInfo()
```

Get information about the most recently previewed Media Explorer file. filename: last played file name. filemode: &1:insert on new track, &2:insert into sampler, &8:tempo sync 1x, &16:tempo sync 0.5x, &32:tempo sync 2x, &64:do not preserve pitch when changing playrate, &128:loop selection exists, &256:time selection exists, &512:apply pitch/rate adjustment on insert, &1024:apply volume adjustment on insert, &2048:apply normalization on insert, &8192:reverse preview. startpct/endpct: time selection in [0.0, 1.0]. pitchshift/voladj/rateadj: current pitch/volume/playrate preview adjustments. srcbpm: source media tempo. extrainfo: currently unused.
## MediaItemDescendsFromTrack
```
integer reaper.MediaItemDescendsFromTrack(MediaItem item, MediaTrack track)
```

Returns 1 if the track holds the item, 2 if the track is a folder containing the track that holds the item, etc.
## Menu_GetHash
```
boolean retval, string hash = reaper.Menu_GetHash(string menuname, integer flag)
```

Get a string that only changes when menu/toolbar entries are added or removed (not re-ordered). Can be used to determine if a customized menu/toolbar differs from the default, or if the default changed after a menu/toolbar was customized. flag==0: current default menu/toolbar; flag==1: current customized menu/toolbar; flag==2: default menu/toolbar at the time the current menu/toolbar was most recently customized, if it was customized in REAPER v7.08 or later.
## MIDI_CountEvts
```
integer retval, integer notecnt, integer ccevtcnt, integer textsyxevtcnt = reaper.MIDI_CountEvts(MediaItem_Take take)
```

Count the number of notes, CC events, and text/sysex events in a given MIDI item.
## MIDI_DeleteCC
```
boolean reaper.MIDI_DeleteCC(MediaItem_Take take, integer ccidx)
```

Delete a MIDI CC event.
## MIDI_DeleteEvt
```
boolean reaper.MIDI_DeleteEvt(MediaItem_Take take, integer evtidx)
```

Delete a MIDI event.
## MIDI_DeleteNote
```
boolean reaper.MIDI_DeleteNote(MediaItem_Take take, integer noteidx)
```

Delete a MIDI note.
## MIDI_DeleteTextSysexEvt
```
boolean reaper.MIDI_DeleteTextSysexEvt(MediaItem_Take take, integer textsyxevtidx)
```

Delete a MIDI text or sysex event.
## MIDI_DisableSort
```
reaper.MIDI_DisableSort(MediaItem_Take take)
```

Disable sorting for all MIDI insert, delete, get and set functions, until MIDI_Sort is called.
## MIDI_EnumSelCC
```
integer reaper.MIDI_EnumSelCC(MediaItem_Take take, integer ccidx)
```

Returns the index of the next selected MIDI CC event after ccidx (-1 if there are no more selected events).
## MIDI_EnumSelEvts
```
integer reaper.MIDI_EnumSelEvts(MediaItem_Take take, integer evtidx)
```

Returns the index of the next selected MIDI event after evtidx (-1 if there are no more selected events).
## MIDI_EnumSelNotes
```
integer reaper.MIDI_EnumSelNotes(MediaItem_Take take, integer noteidx)
```

Returns the index of the next selected MIDI note after noteidx (-1 if there are no more selected events).
## MIDI_EnumSelTextSysexEvts
```
integer reaper.MIDI_EnumSelTextSysexEvts(MediaItem_Take take, integer textsyxidx)
```

Returns the index of the next selected MIDI text/sysex event after textsyxidx (-1 if there are no more selected events).
## MIDI_GetAllEvts
```
boolean retval, string buf = reaper.MIDI_GetAllEvts(MediaItem_Take take)
```

Get all MIDI data. MIDI buffer is returned as a list of { int offset, char flag, int msglen, unsigned char msg[] }.
offset: MIDI ticks from previous event
flag: &1=selected &2=muted
flag high 4 bits for CC shape: &16=linear, &32=slow start/end, &16|32=fast start, &64=fast end, &64|16=bezier
msg: the MIDI message.
A meta-event of type 0xF followed by 'CCBZ ' and 5 more bytes represents bezier curve data for the previous MIDI event: 1 byte for the bezier type (usually 0) and 4 bytes for the bezier tension as a float.
For tick intervals longer than a 32 bit word can represent, zero-length meta events may be placed between valid events.
See MIDI_SetAllEvts.
## MIDI_GetCC
```
boolean retval, boolean selected, boolean muted, number ppqpos, integer chanmsg, integer chan, integer msg2, integer msg3 = reaper.MIDI_GetCC(MediaItem_Take take, integer ccidx)
```

Get MIDI CC event properties.
## MIDI_GetCCShape
```
boolean retval, integer shape, number beztension = reaper.MIDI_GetCCShape(MediaItem_Take take, integer ccidx)
```

Get CC shape and bezier tension. See MIDI_GetCC, MIDI_SetCCShape
## MIDI_GetEvt
```
boolean retval, boolean selected, boolean muted, number ppqpos, string msg = reaper.MIDI_GetEvt(MediaItem_Take take, integer evtidx)
```

Get MIDI event properties.
## MIDI_GetGrid
```
number retval, optional number swing, optional number noteLen = reaper.MIDI_GetGrid(MediaItem_Take take)
```

Returns the most recent MIDI editor grid size for this MIDI take, in QN. Swing is between 0 and 1. Note length is 0 if it follows the grid size.
## MIDI_GetHash
```
boolean retval, string hash = reaper.MIDI_GetHash(MediaItem_Take take, boolean notesonly)
```

Get a string that only changes when the MIDI data changes. If notesonly==true, then the string changes only when the MIDI notes change. See MIDI_GetTrackHash
## MIDI_GetNote
```
boolean retval, boolean selected, boolean muted, number startppqpos, number endppqpos, integer chan, integer pitch, integer vel = reaper.MIDI_GetNote(MediaItem_Take take, integer noteidx)
```

Get MIDI note properties.
## MIDI_GetPPQPos_EndOfMeasure
```
number reaper.MIDI_GetPPQPos_EndOfMeasure(MediaItem_Take take, number ppqpos)
```

Returns the MIDI tick (ppq) position corresponding to the end of the measure.
## MIDI_GetPPQPos_StartOfMeasure
```
number reaper.MIDI_GetPPQPos_StartOfMeasure(MediaItem_Take take, number ppqpos)
```

Returns the MIDI tick (ppq) position corresponding to the start of the measure.
## MIDI_GetPPQPosFromProjQN
```
number reaper.MIDI_GetPPQPosFromProjQN(MediaItem_Take take, number projqn)
```

Returns the MIDI tick (ppq) position corresponding to a specific project time in quarter notes.
## MIDI_GetPPQPosFromProjTime
```
number reaper.MIDI_GetPPQPosFromProjTime(MediaItem_Take take, number projtime)
```

Returns the MIDI tick (ppq) position corresponding to a specific project time in seconds.
## MIDI_GetProjQNFromPPQPos
```
number reaper.MIDI_GetProjQNFromPPQPos(MediaItem_Take take, number ppqpos)
```

Returns the project time in quarter notes corresponding to a specific MIDI tick (ppq) position.
## MIDI_GetProjTimeFromPPQPos
```
number reaper.MIDI_GetProjTimeFromPPQPos(MediaItem_Take take, number ppqpos)
```

Returns the project time in seconds corresponding to a specific MIDI tick (ppq) position.
## MIDI_GetRecentInputEvent
```
integer retval, string buf, integer ts, integer devIdx, number projPos, integer projLoopCnt = reaper.MIDI_GetRecentInputEvent(integer idx)
```

Gets a recent MIDI input event from the global history. idx=0 for the most recent event, which also latches to the latest MIDI event state (to get a more recent list, calling with idx=0 is necessary). idx=1 next most recent event, returns a non-zero sequence number for the event, or zero if no more events. tsOut will be set to the timestamp in samples relative to the current position (0 is current, -48000 is one second ago, etc). devIdxOut will have the low 16 bits set to the input device index, and 0x10000 will be set if device was enabled only for control. projPosOut will be set to project position in seconds if project was playing back at time of event, otherwise -1. Large SysEx events will not be included in this event list.
## MIDI_GetScale
```
boolean retval, integer root, integer scale, string name = reaper.MIDI_GetScale(MediaItem_Take take)
```

Get the active scale in the media source, if any. root 0=C, 1=C#, etc. scale &0x1=root, &0x2=minor 2nd, &0x4=major 2nd, &0x8=minor 3rd, &0xF=fourth, etc.
## MIDI_GetTextSysexEvt
```
boolean retval, optional boolean selected, optional boolean muted, optional number ppqpos, optional integer type, optional string msg = reaper.MIDI_GetTextSysexEvt(MediaItem_Take take, integer textsyxevtidx, optional boolean selected, optional boolean muted, optional number ppqpos, optional integer type, optional string msg)
```

Get MIDI meta-event properties. Allowable types are -1:sysex (msg should not include bounding F0..F7), 1-14:MIDI text event types, 15=REAPER notation event. For all other meta-messages, type is returned as -2 and msg returned as all zeroes. See MIDI_GetEvt.
## MIDI_GetTrackHash
```
boolean retval, string hash = reaper.MIDI_GetTrackHash(MediaTrack track, boolean notesonly)
```

Get a string that only changes when the MIDI data changes. If notesonly==true, then the string changes only when the MIDI notes change. See MIDI_GetHash
## midi_init
```
reaper.midi_init(integer force_reinit_input, integer force_reinit_output)
```

Opens MIDI devices as configured in preferences. force_reinit_input and force_reinit_output force a particular device index to close/re-open (pass -1 to not force any devices to reopen).
## MIDI_InsertCC
```
boolean reaper.MIDI_InsertCC(MediaItem_Take take, boolean selected, boolean muted, number ppqpos, integer chanmsg, integer chan, integer msg2, integer msg3)
```

Insert a new MIDI CC event.
## MIDI_InsertEvt
```
boolean reaper.MIDI_InsertEvt(MediaItem_Take take, boolean selected, boolean muted, number ppqpos, string bytestr)
```

Insert a new MIDI event.
## MIDI_InsertNote
```
boolean reaper.MIDI_InsertNote(MediaItem_Take take, boolean selected, boolean muted, number startppqpos, number endppqpos, integer chan, integer pitch, integer vel, optional boolean noSortIn)
```

Insert a new MIDI note. Set noSort if inserting multiple events, then call MIDI_Sort when done.
## MIDI_InsertTextSysexEvt
```
boolean reaper.MIDI_InsertTextSysexEvt(MediaItem_Take take, boolean selected, boolean muted, number ppqpos, integer type, string bytestr)
```

Insert a new MIDI text or sysex event. Allowable types are -1:sysex (msg should not include bounding F0..F7), 1-14:MIDI text event types, 15=REAPER notation event.
## MIDI_RefreshEditors
```
reaper.MIDI_RefreshEditors(MediaItem_Take tk)
```

Synchronously updates any open MIDI editors for MIDI take
## midi_reinit
```
reaper.midi_reinit()
```

Reset (close and re-open) all MIDI devices
## MIDI_SelectAll
```
reaper.MIDI_SelectAll(MediaItem_Take take, boolean select)
```

Select or deselect all MIDI content.
## MIDI_SetAllEvts
```
boolean reaper.MIDI_SetAllEvts(MediaItem_Take take, string buf)
```

Set all MIDI data. MIDI buffer is passed in as a list of { int offset, char flag, int msglen, unsigned char msg[] }.
offset: MIDI ticks from previous event
flag: &1=selected &2=muted
flag high 4 bits for CC shape: &16=linear, &32=slow start/end, &16|32=fast start, &64=fast end, &64|16=bezier
msg: the MIDI message.
A meta-event of type 0xF followed by 'CCBZ ' and 5 more bytes represents bezier curve data for the previous MIDI event: 1 byte for the bezier type (usually 0) and 4 bytes for the bezier tension as a float.
For tick intervals longer than a 32 bit word can represent, zero-length meta events may be placed between valid events.
See MIDI_GetAllEvts.
## MIDI_SetCC
```
boolean reaper.MIDI_SetCC(MediaItem_Take take, integer ccidx, optional boolean selectedIn, optional boolean mutedIn, optional number ppqposIn, optional integer chanmsgIn, optional integer chanIn, optional integer msg2In, optional integer msg3In, optional boolean noSortIn)
```

Set MIDI CC event properties. Properties passed as NULL will not be set. set noSort if setting multiple events, then call MIDI_Sort when done.
## MIDI_SetCCShape
```
boolean reaper.MIDI_SetCCShape(MediaItem_Take take, integer ccidx, integer shape, number beztension, optional boolean noSortIn)
```

Set CC shape and bezier tension. set noSort if setting multiple events, then call MIDI_Sort when done. See MIDI_SetCC, MIDI_GetCCShape
## MIDI_SetEvt
```
boolean reaper.MIDI_SetEvt(MediaItem_Take take, integer evtidx, optional boolean selectedIn, optional boolean mutedIn, optional number ppqposIn, optional string msg, optional boolean noSortIn)
```

Set MIDI event properties. Properties passed as NULL will not be set. set noSort if setting multiple events, then call MIDI_Sort when done.
## MIDI_SetItemExtents
```
boolean reaper.MIDI_SetItemExtents(MediaItem item, number startQN, number endQN)
```

Set the start/end positions of a media item that contains a MIDI take.
## MIDI_SetNote
```
boolean reaper.MIDI_SetNote(MediaItem_Take take, integer noteidx, optional boolean selectedIn, optional boolean mutedIn, optional number startppqposIn, optional number endppqposIn, optional integer chanIn, optional integer pitchIn, optional integer velIn, optional boolean noSortIn)
```

Set MIDI note properties. Properties passed as NULL (or negative values) will not be set. Set noSort if setting multiple events, then call MIDI_Sort when done. Setting multiple note start positions at once is done more safely by deleting and re-inserting the notes.
## MIDI_SetTextSysexEvt
```
boolean reaper.MIDI_SetTextSysexEvt(MediaItem_Take take, integer textsyxevtidx, optional boolean selectedIn, optional boolean mutedIn, optional number ppqposIn, optional integer typeIn, optional string msg, optional boolean noSortIn)
```

Set MIDI text or sysex event properties. Properties passed as NULL will not be set. Allowable types are -1:sysex (msg should not include bounding F0..F7), 1-14:MIDI text event types, 15=REAPER notation event. set noSort if setting multiple events, then call MIDI_Sort when done.
## MIDI_Sort
```
reaper.MIDI_Sort(MediaItem_Take take)
```

Sort MIDI events after multiple calls to MIDI_SetNote, MIDI_SetCC, etc.
## MIDIEditor_EnumTakes
```
MediaItem_Take reaper.MIDIEditor_EnumTakes(HWND midieditor, integer takeindex, boolean editable_only)
```

list the takes that are currently being edited in this MIDI editor, starting with the active take. See MIDIEditor_GetTake
## MIDIEditor_GetActive
```
HWND reaper.MIDIEditor_GetActive()
```

get a pointer to the focused MIDI editor window
see MIDIEditor_GetMode, MIDIEditor_OnCommand
## MIDIEditor_GetMode
```
integer reaper.MIDIEditor_GetMode(HWND midieditor)
```

get the mode of a MIDI editor (0=piano roll, 1=event list, -1=invalid editor)
see MIDIEditor_GetActive, MIDIEditor_OnCommand
## MIDIEditor_GetSetting_int
```
integer reaper.MIDIEditor_GetSetting_int(HWND midieditor, string setting_desc)
```

Get settings from a MIDI editor. setting_desc can be:
snap_enabled: returns 0 or 1
active_note_row: returns 0-127
last_clicked_cc_lane: returns 0-127=CC, 0x100|(0-31)=14-bit CC, 0x200=velocity, 0x201=pitch, 0x202=program, 0x203=channel pressure, 0x204=bank/program select, 0x205=text, 0x206=sysex, 0x207=off velocity, 0x208=notation events, 0x209=aftertouch, 0x210=media item lane
default_note_vel: returns 0-127
default_note_chan: returns 0-15
default_note_len: returns default length in MIDI ticks
scale_enabled: returns 0-1
scale_root: returns 0-12 (0=C)
list_cnt: if viewing list view, returns event count
if setting_desc is unsupported, the function returns -1.
See MIDIEditor_SetSetting_int, MIDIEditor_GetActive, MIDIEditor_GetSetting_str
## MIDIEditor_GetSetting_str
```
boolean retval, string buf = reaper.MIDIEditor_GetSetting_str(HWND midieditor, string setting_desc)
```

Get settings from a MIDI editor. setting_desc can be:
last_clicked_cc_lane: returns text description ("velocity", "pitch", etc)
scale: returns the scale record, for example "102034050607" for a major scale
list_X: if viewing list view, returns string describing event at row X (0-based). String will have a list of key=value pairs, e.g. 'pos=4.0 len=4.0 offvel=127 msg=90317F'. pos/len times are in QN, len/offvel may not be present if event is not a note. other keys which may be present include pos_pq/len_pq, sel, mute, ccval14, ccshape, ccbeztension.
if setting_desc is unsupported, the function returns false.
See MIDIEditor_GetActive, MIDIEditor_GetSetting_int
## MIDIEditor_GetTake
```
MediaItem_Take reaper.MIDIEditor_GetTake(HWND midieditor)
```

get the take that is currently being edited in this MIDI editor. see MIDIEditor_EnumTakes
## MIDIEditor_LastFocused_OnCommand
```
boolean reaper.MIDIEditor_LastFocused_OnCommand(integer command_id, boolean islistviewcommand)
```

Send an action command to the last focused MIDI editor. Returns false if there is no MIDI editor open, or if the view mode (piano roll or event list) does not match the input.
see MIDIEditor_OnCommand
## MIDIEditor_OnCommand
```
boolean reaper.MIDIEditor_OnCommand(HWND midieditor, integer command_id)
```

Send an action command to a MIDI editor. Returns false if the supplied MIDI editor pointer is not valid (not an open MIDI editor).
see MIDIEditor_GetActive, MIDIEditor_LastFocused_OnCommand
## MIDIEditor_SetSetting_int
```
boolean reaper.MIDIEditor_SetSetting_int(HWND midieditor, string setting_desc, integer setting)
```

Set settings for a MIDI editor. setting_desc can be:
active_note_row: 0-127
See MIDIEditor_GetSetting_int
## MIDIEditorFlagsForTrack
```
integer pitchwheelrange, integer flags = reaper.MIDIEditorFlagsForTrack(MediaTrack track, integer pitchwheelrange, integer flags, boolean is_set)
```

Get or set MIDI editor settings for this track. pitchwheelrange: semitones up or down. flags &1: snap pitch lane edits to semitones if pitchwheel range is defined.
## mkpanstr
```
string strNeed64 = reaper.mkpanstr(string strNeed64, number pan)
```

No description available.
## mkvolpanstr
```
string strNeed64 = reaper.mkvolpanstr(string strNeed64, number vol, number pan)
```

No description available.
## mkvolstr
```
string strNeed64 = reaper.mkvolstr(string strNeed64, number vol)
```

No description available.
## MoveEditCursor
```
reaper.MoveEditCursor(number adjamt, boolean dosel)
```

No description available.
## MoveMediaItemToTrack
```
boolean reaper.MoveMediaItemToTrack(MediaItem item, MediaTrack desttr)
```

returns TRUE if move succeeded
## MuteAllTracks
```
reaper.MuteAllTracks(boolean mute)
```

No description available.
## my_getViewport
```
reaper.my_getViewport(integerr.left, integerr.top, integerr.right, integerr.bot, integer sr.left, integer sr.top, integer sr.right, integer sr.bot, boolean wantWorkArea)
```

No description available.
## NamedCommandLookup
```
integer reaper.NamedCommandLookup(string command_name)
```

Get the command ID number for named command that was registered by an extension such as "_SWS_ABOUT" or "_113088d11ae641c193a2b7ede3041ad5" for a ReaScript or a custom action.
## OnPauseButton
```
reaper.OnPauseButton()
```

direct way to simulate pause button hit
## OnPauseButtonEx
```
reaper.OnPauseButtonEx(ReaProject proj)
```

direct way to simulate pause button hit
## OnPlayButton
```
reaper.OnPlayButton()
```

direct way to simulate play button hit
## OnPlayButtonEx
```
reaper.OnPlayButtonEx(ReaProject proj)
```

direct way to simulate play button hit
## OnStopButton
```
reaper.OnStopButton()
```

direct way to simulate stop button hit
## OnStopButtonEx
```
reaper.OnStopButtonEx(ReaProject proj)
```

direct way to simulate stop button hit
## OpenColorThemeFile
```
boolean reaper.OpenColorThemeFile(string fn)
```

No description available.
## OpenMediaExplorer
```
HWND reaper.OpenMediaExplorer(string mediafn, boolean play)
```

Opens mediafn in the Media Explorer, play=true will play the file immediately (or toggle playback if mediafn was already open), =false will just select it.
## OscLocalMessageToHost
```
reaper.OscLocalMessageToHost(string message, optional number valueIn)
```

Send an OSC message directly to REAPER. The value argument may be NULL. The message will be matched against the default OSC patterns.
## parse_timestr
```
number reaper.parse_timestr(string buf)
```

Parse hh:mm:ss.sss time string, return time in seconds (or 0.0 on error). See parse_timestr_pos, parse_timestr_len.
## parse_timestr_len
```
number reaper.parse_timestr_len(string buf, number offset, integer modeoverride)
```

time formatting mode overrides: -1=proj default.
0=time
1=measures.beats + time
2=measures.beats
3=seconds
4=samples
5=h:m:s:f
## parse_timestr_pos
```
number reaper.parse_timestr_pos(string buf, integer modeoverride)
```

Parse time string, time formatting mode overrides: -1=proj default.
0=time
1=measures.beats + time
2=measures.beats
3=seconds
4=samples
5=h:m:s:f
## parsepanstr
```
number reaper.parsepanstr(string str)
```

No description available.
## PCM_Sink_Enum
```
integer retval, string descstr = reaper.PCM_Sink_Enum(integer idx)
```

No description available.
## PCM_Sink_GetExtension
```
string reaper.PCM_Sink_GetExtension(string data)
```

No description available.
## PCM_Sink_ShowConfig
```
HWND reaper.PCM_Sink_ShowConfig(string cfg, HWND hwndParent)
```

No description available.
## PCM_Source_BuildPeaks
```
integer reaper.PCM_Source_BuildPeaks(PCM_source src, integer mode)
```

Calls and returns PCM_source::PeaksBuild_Begin() if mode=0, PeaksBuild_Run() if mode=1, and PeaksBuild_Finish() if mode=2. Normal use is to call PCM_Source_BuildPeaks(src,0), and if that returns nonzero, call PCM_Source_BuildPeaks(src,1) periodically until it returns zero (it returns the percentage of the file remaining), then call PCM_Source_BuildPeaks(src,2) to finalize. If PCM_Source_BuildPeaks(src,0) returns zero, then no further action is necessary.
## PCM_Source_CreateFromFile
```
PCM_source reaper.PCM_Source_CreateFromFile(string filename)
```

See PCM_Source_CreateFromFileEx.
## PCM_Source_CreateFromFileEx
```
PCM_source reaper.PCM_Source_CreateFromFileEx(string filename, boolean forcenoMidiImp)
```

Create a PCM_source from filename, and override pref of MIDI files being imported as in-project MIDI events.
## PCM_Source_CreateFromType
```
PCM_source reaper.PCM_Source_CreateFromType(string sourcetype)
```

Create a PCM_source from a "type" (use this if you're going to load its state via LoadState/ProjectStateContext).
Valid types include "WAVE", "MIDI", or whatever plug-ins define as well.
## PCM_Source_Destroy
```
reaper.PCM_Source_Destroy(PCM_source src)
```

Deletes a PCM_source -- be sure that you remove any project reference before deleting a source
## PCM_Source_GetPeaks
```
integer reaper.PCM_Source_GetPeaks(PCM_source src, number peakrate, number starttime, integer numchannels, integer numsamplesperchannel, integer want_extra_type, reaper.array buf)
```

Gets block of peak samples to buf. Note that the peak samples are interleaved, but in two or three blocks (maximums, then minimums, then extra). Return value has 20 bits of returned sample count, then 4 bits of output_mode (0xf00000), then a bit to signify whether extra_type was available (0x1000000). extra_type can be 115 ('s') for spectral information, which will return peak samples as integers with the low 15 bits frequency, next 14 bits tonality.
## PCM_Source_GetSectionInfo
```
boolean retval, number offs, number len, boolean rev = reaper.PCM_Source_GetSectionInfo(PCM_source src)
```

If a section/reverse block, retrieves offset/len/reverse. return true if success
## PluginWantsAlwaysRunFx
```
reaper.PluginWantsAlwaysRunFx(integer amt)
```

No description available.
## PreventUIRefresh
```
reaper.PreventUIRefresh(integer prevent_count)
```

adds prevent_count to the UI refresh prevention state; always add then remove the same amount, or major disfunction will occur
## PromptForAction
```
integer reaper.PromptForAction(integer session_mode, integer init_id, integer section_id)
```

Uses the action list to choose an action. Call with session_mode=1 to create a session (init_id will be the initial action to select, or 0), then poll with session_mode=0, checking return value for user-selected action (will return 0 if no action selected yet, or -1 if the action window is no longer available). When finished, call with session_mode=-1.
## ReaScriptError
```
reaper.ReaScriptError(string errmsg)
```

Causes REAPER to display the error message after the current ReaScript finishes. If called within a Lua context and errmsg has a ! prefix, script execution will be terminated.
## RecursiveCreateDirectory
```
integer reaper.RecursiveCreateDirectory(string path, integer ignored)
```

returns positive value on success, 0 on failure.
## reduce_open_files
```
integer reaper.reduce_open_files(integer flags)
```

garbage-collects extra open files and closes them. if flags has 1 set, this is done incrementally (call this from a regular timer, if desired). if flags has 2 set, files are aggressively closed (they may need to be re-opened very soon). returns number of files closed by this call.
## RefreshToolbar
```
reaper.RefreshToolbar(integer command_id)
```

See RefreshToolbar2.
## RefreshToolbar2
```
reaper.RefreshToolbar2(integer section_id, integer command_id)
```

Refresh the toolbar button states of a toggle action.
## relative_fn
```
string out = reaper.relative_fn(string in, string out)
```

Makes a filename "in" relative to the current project, if any.
## RemoveTrackSend
```
boolean reaper.RemoveTrackSend(MediaTrack tr, integer category, integer sendidx)
```

Remove a send/receive/hardware output, return true on success. category is <0 for receives, 0=sends, >0 for hardware outputs. See CreateTrackSend, GetSetTrackSendInfo, GetTrackSendInfo_Value, SetTrackSendInfo_Value, GetTrackNumSends.
## RenderFileSection
```
boolean reaper.RenderFileSection(string source_filename, string target_filename, number start_percent, number end_percent, number playrate)
```

Not available while playing back.
## ReorderSelectedTracks
```
boolean reaper.ReorderSelectedTracks(integer beforeTrackIdx, integer makePrevFolder)
```

Moves all selected tracks to immediately above track specified by index beforeTrackIdx, returns false if no tracks were selected. makePrevFolder=0 for normal, 1 = as child of track preceding track specified by beforeTrackIdx, 2 = if track preceding track specified by beforeTrackIdx is last track in folder, extend folder
## Resample_EnumModes
```
string reaper.Resample_EnumModes(integer mode)
```

No description available.
## resolve_fn
```
string out = reaper.resolve_fn(string in, string out)
```

See resolve_fn2.
## resolve_fn2
```
string out = reaper.resolve_fn2(string in, string out, optional string checkSubDir)
```

Resolves a filename "in" by using project settings etc. If no file found, out will be a copy of in.
## ReverseNamedCommandLookup
```
string reaper.ReverseNamedCommandLookup(integer command_id)
```

Get the named command for the given command ID. The returned string will not start with '_' (e.g. it will return "SWS_ABOUT"), it will be NULL if command_id is a native action.
## ScaleFromEnvelopeMode
```
number reaper.ScaleFromEnvelopeMode(integer scaling_mode, number val)
```

See GetEnvelopeScalingMode.
## ScaleToEnvelopeMode
```
number reaper.ScaleToEnvelopeMode(integer scaling_mode, number val)
```

See GetEnvelopeScalingMode.
## SectionFromUniqueID
```
KbdSectionInfo reaper.SectionFromUniqueID(integer uniqueID)
```

No description available.
## SelectAllMediaItems
```
reaper.SelectAllMediaItems(ReaProject proj, boolean selected)
```

No description available.
## SelectProjectInstance
```
reaper.SelectProjectInstance(ReaProject proj)
```

No description available.
## SendMIDIMessageToHardware
```
reaper.SendMIDIMessageToHardware(integer output, string msg)
```

Sends a MIDI message to output device specified by output. Message is sent in immediate mode. Lua example of how to pack the message string:
sysex = { 0xF0, 0x00, 0xF7 }
msg = ""
for i=1, #sysex do msg = msg .. string.char(sysex[i]) end
## SetActiveTake
```
reaper.SetActiveTake(MediaItem_Take take)
```

set this take active in this media item
## SetAutomationMode
```
reaper.SetAutomationMode(integer mode, boolean onlySel)
```

sets all or selected tracks to mode.
## SetCurrentBPM
```
reaper.SetCurrentBPM(ReaProject __proj, number bpm, boolean wantUndo)
```

set current BPM in project, set wantUndo=true to add undo point
## SetCursorContext
```
reaper.SetCursorContext(integer mode, TrackEnvelope envIn)
```

You must use this to change the focus programmatically. mode=0 to focus track panels, 1 to focus the arrange window, 2 to focus the arrange window and select env (or env==NULL to clear the current track/take envelope selection)
## SetEditCurPos
```
reaper.SetEditCurPos(number time, boolean moveview, boolean seekplay)
```

No description available.
## SetEditCurPos2
```
reaper.SetEditCurPos2(ReaProject proj, number time, boolean moveview, boolean seekplay)
```

No description available.
## SetEnvelopePoint
```
boolean reaper.SetEnvelopePoint(TrackEnvelope envelope, integer ptidx, optional number timeIn, optional number valueIn, optional integer shapeIn, optional number tensionIn, optional boolean selectedIn, optional boolean noSortIn)
```

Set attributes of an envelope point. Values that are not supplied will be ignored. If setting multiple points at once, set noSort=true, and call Envelope_SortPoints when done. See SetEnvelopePointEx.
## SetEnvelopePointEx
```
boolean reaper.SetEnvelopePointEx(TrackEnvelope envelope, integer autoitem_idx, integer ptidx, optional number timeIn, optional number valueIn, optional integer shapeIn, optional number tensionIn, optional boolean selectedIn, optional boolean noSortIn)
```

Set attributes of an envelope point. Values that are not supplied will be ignored. If setting multiple points at once, set noSort=true, and call Envelope_SortPoints when done.
autoitem_idx=-1 for the underlying envelope, 0 for the first automation item on the envelope, etc.
For automation items, pass autoitem_idx|0x10000000 to base ptidx on the number of points in one full loop iteration,
even if the automation item is trimmed so that not all points are visible.
Otherwise, ptidx will be based on the number of visible points in the automation item, including all loop iterations.
See CountEnvelopePointsEx, GetEnvelopePointEx, InsertEnvelopePointEx, DeleteEnvelopePointEx.
## SetEnvelopeStateChunk
```
boolean reaper.SetEnvelopeStateChunk(TrackEnvelope env, string str, boolean isundo)
```

Sets the RPPXML state of an envelope, returns true if successful. Undo flag is a performance/caching hint.
## SetExtState
```
reaper.SetExtState(string section, string key, string value, boolean persist)
```

Set the extended state value for a specific section and key. persist=true means the value should be stored and reloaded the next time REAPER is opened. See GetExtState, DeleteExtState, HasExtState.
## SetGlobalAutomationOverride
```
reaper.SetGlobalAutomationOverride(integer mode)
```

mode: see GetGlobalAutomationOverride
## SetItemStateChunk
```
boolean reaper.SetItemStateChunk(MediaItem item, string str, boolean isundo)
```

Sets the RPPXML state of an item, returns true if successful. Undo flag is a performance/caching hint.
## SetMasterTrackVisibility
```
integer reaper.SetMasterTrackVisibility(integer flag)
```

set &1 to show the master track in the TCP, &2 to HIDE in the mixer. Returns the previous visibility state. See GetMasterTrackVisibility.
## SetMediaItemInfo_Value
```
boolean reaper.SetMediaItemInfo_Value(MediaItem item, string parmname, number newvalue)
```

Set media item numerical-value attributes.
B_MUTE : bool * : muted (item solo overrides). setting this value will clear C_MUTE_SOLO.
B_MUTE_ACTUAL : bool * : muted (ignores solo). setting this value will not affect C_MUTE_SOLO.
C_LANEPLAYS : char * : on fixed lane tracks, 0=this item lane does not play, 1=this item lane plays exclusively, 2=this item lane plays and other lanes also play, -1=this item is on a non-visible, non-playing lane on a formerly fixed-lane track (read-only)
C_MUTE_SOLO : char * : solo override (-1=soloed, 0=no override, 1=unsoloed). note that this API does not automatically unsolo other items when soloing (nor clear the unsolos when clearing the last soloed item), it must be done by the caller via action or via this API.
B_LOOPSRC : bool * : loop source
B_ALLTAKESPLAY : bool * : all takes play
B_UISEL : bool * : selected in arrange view
C_BEATATTACHMODE : char * : item timebase, -1=track or project default, 1=beats (position, length, rate), 2=beats (position only). for auto-stretch timebase: C_BEATATTACHMODE=1, C_AUTOSTRETCH=1
C_AUTOSTRETCH: : char * : auto-stretch at project tempo changes, 1=enabled, requires C_BEATATTACHMODE=1
C_LOCK : char * : locked, &1=locked
D_VOL : double * : item volume, 0=-inf, 0.5=-6dB, 1=+0dB, 2=+6dB, etc
D_POSITION : double * : item position in seconds
D_LENGTH : double * : item length in seconds
D_SNAPOFFSET : double * : item snap offset in seconds
D_FADEINLEN : double * : item manual fadein length in seconds
D_FADEOUTLEN : double * : item manual fadeout length in seconds
D_FADEINDIR : double * : item fadein curvature, -1..1
D_FADEOUTDIR : double * : item fadeout curvature, -1..1
D_FADEINLEN_AUTO : double * : item auto-fadein length in seconds, -1=no auto-fadein
D_FADEOUTLEN_AUTO : double * : item auto-fadeout length in seconds, -1=no auto-fadeout
C_FADEINSHAPE : int * : fadein shape, 0..6, 0=linear
C_FADEOUTSHAPE : int * : fadeout shape, 0..6, 0=linear
I_GROUPID : int * : group ID, 0=no group
I_LASTY : int * : Y-position (relative to top of track) in pixels (read-only)
I_LASTH : int * : height in pixels (read-only)
I_CUSTOMCOLOR : int * : custom color, OS dependent color|0x1000000 (i.e. ColorToNative(r,g,b)|0x1000000). If you do not |0x1000000, then it will not be used, but will store the color
I_CURTAKE : int * : active take number
IP_ITEMNUMBER : int : item number on this track (read-only, returns the item number directly)
F_FREEMODE_Y : float * : free item positioning or fixed lane Y-position. 0=top of track, 1.0=bottom of track
F_FREEMODE_H : float * : free item positioning or fixed lane height. 0.5=half the track height, 1.0=full track height
I_FIXEDLANE : int * : fixed lane of item (fine to call with setNewValue, but returned value is read-only)
B_FIXEDLANE_HIDDEN : bool * : true if displaying only one fixed lane and this item is in a different lane (read-only)
## SetMediaItemLength
```
boolean reaper.SetMediaItemLength(MediaItem item, number length, boolean refreshUI)
```

Redraws the screen only if refreshUI == true.
See UpdateArrange().
## SetMediaItemPosition
```
boolean reaper.SetMediaItemPosition(MediaItem item, number position, boolean refreshUI)
```

Redraws the screen only if refreshUI == true.
See UpdateArrange().
## SetMediaItemSelected
```
reaper.SetMediaItemSelected(MediaItem item, boolean selected)
```

No description available.
## SetMediaItemTake_Source
```
boolean reaper.SetMediaItemTake_Source(MediaItem_Take take, PCM_source source)
```

Set media source of media item take. The old source will not be destroyed, it is the caller's responsibility to retrieve it and destroy it after. If source already exists in any project, it will be duplicated before being set. C/C++ code should not use this and instead use GetSetMediaItemTakeInfo() with P_SOURCE to manage ownership directly.
## SetMediaItemTakeInfo_Value
```
boolean reaper.SetMediaItemTakeInfo_Value(MediaItem_Take take, string parmname, number newvalue)
```

Set media item take numerical-value attributes.
D_STARTOFFS : double * : start offset in source media, in seconds
D_VOL : double * : take volume, 0=-inf, 0.5=-6dB, 1=+0dB, 2=+6dB, etc, negative if take polarity is flipped
D_PAN : double * : take pan, -1..1
D_PANLAW : double * : take pan law, -1=default, 0.5=-6dB, 1.0=+0dB, etc
D_PLAYRATE : double * : take playback rate, 0.5=half speed, 1=normal, 2=double speed, etc
D_PITCH : double * : take pitch adjustment in semitones, -12=one octave down, 0=normal, +12=one octave up, etc
B_PPITCH : bool * : preserve pitch when changing playback rate
I_LASTY : int * : Y-position (relative to top of track) in pixels (read-only)
I_LASTH : int * : height in pixels (read-only)
I_CHANMODE : int * : channel mode, 0=normal, 1=reverse stereo, 2=downmix, 3=left, 4=right
I_PITCHMODE : int * : pitch shifter mode, -1=project default, otherwise high 2 bytes=shifter, low 2 bytes=parameter
I_STRETCHFLAGS : int * : stretch marker flags (&7 mask for mode override: 0=default, 1=balanced, 2/3/6=tonal, 4=transient, 5=no pre-echo)
F_STRETCHFADESIZE : float * : stretch marker fade size in seconds (0.0025 default)
I_RECPASSID : int * : record pass ID
I_TAKEFX_NCH : int * : number of internal audio channels for per-take FX to use (OK to call with setNewValue, but the returned value is read-only)
I_CUSTOMCOLOR : int * : custom color, OS dependent color|0x1000000 (i.e. ColorToNative(r,g,b)|0x1000000). If you do not |0x1000000, then it will not be used, but will store the color
IP_SPECEDIT:CNT : int : spectral edit count (read-only)
IP_SPECEDIT:DELETE:x : int : read or write this key to remove the spectral edit specified
IP_SPECEDIT:ADD : int : read or write this key to add a new spectral edit (returns index)
IP_SPECEDIT:SORT : int : read or write this key to re-sort spectral edits (be sure to do this following a position change or insert of new edit)
I_SPECEDIT:FFT_SIZE : int * : FFT size used by spectral edits for this take
D_SPECEDIT:x:POSITION : double * : position of spectral edit start (changing this requires a resort of spectral edits)
D_SPECEDIT:x:LENGTH : double * : length of spectral edit
F_SPECEDIT:x:GAIN : float * : gain of spectral edit
F_SPECEDIT:x:FADE_IN : float * : fade-in size 0..1
F_SPECEDIT:x:FADE_OUT : float * : fade-out size 0..1
F_SPECEDIT:x:FADE_LOW : float * : fade-lf size 0..1
F_SPECEDIT:x:FADE_HI : float * : fade-hf size 0..1
I_SPECEDIT:x:CHAN : int * : channel index, -1 for omni
I_SPECEDIT:x:FLAGS : int * : flags, &1=bypassed, &2=solo
F_SPECEDIT:x:GATE_THRESH : float * : gate threshold
F_SPECEDIT:x:GATE_FLOOR : float * : gate floor
F_SPECEDIT:x:COMP_THRESH : float * : comp threshold
F_SPECEDIT:x:COMP_RATIO : float * : comp ratio
B_SPECEDIT:x:SELECTED : bool * : selection state
I_SPECEDIT:x:TOPFREQ_CNT : int * : (read-only) number of top frequency-points
I_SPECEDIT:x:TOPFREQ_ADD:pos:val : int * : reading or writing will insert top frequency-point with position/value pair, returns index
I_SPECEDIT:x:TOPFREQ_DEL:y : int * : reading or writing will delete top frequency-point y. there will always be at least one point.
F_SPECEDIT:x:TOPFREQ_POS:y : float * : (read-only) get position of top frequency-point y
F_SPECEDIT:x:TOPFREQ_FREQ:y : float * : (read-only) get frequency of top frequency-point y
I_SPECEDIT:x:BOTFREQ_CNT : int * : number of bottom frequency-points
I_SPECEDIT:x:BOTFREQ_ADD:pos:val : int * : reading or writing will insert bottom frequency-point with position/value pair, returns index
I_SPECEDIT:x:BOTFREQ_DEL:y : int * : reading or writing will delete bottom frequency-point y. there will always be at least one point.
F_SPECEDIT:x:BOTFREQ_POS:y : float * : (read-only) get position of bottom frequency-point y
F_SPECEDIT:x:BOTFREQ_FREQ:y : float * : (read-only) get frequency of bottom frequency-point y
IP_TAKENUMBER : int : take number (read-only, returns the take number directly)
## SetMediaTrackInfo_Value
```
boolean reaper.SetMediaTrackInfo_Value(MediaTrack tr, string parmname, number newvalue)
```

Set track numerical-value attributes.
B_MUTE : bool * : muted
B_PHASE : bool * : track phase inverted
B_RECMON_IN_EFFECT : bool * : record monitoring in effect (current audio-thread playback state, read-only)
IP_TRACKNUMBER : int : track number 1-based, 0=not found, -1=master track (read-only, returns the int directly)
I_SOLO : int * : soloed, 0=not soloed, 1=soloed, 2=soloed in place, 5=safe soloed, 6=safe soloed in place
B_SOLO_DEFEAT : bool * : when set, if anything else is soloed and this track is not muted, this track acts soloed
I_FXEN : int * : fx enabled, 0=bypassed, !0=fx active
I_RECARM : int * : record armed, 0=not record armed, 1=record armed
I_RECINPUT : int * : record input, <0=no input. if 4096 set, input is MIDI and low 5 bits represent channel (0=all, 1-16=only chan), next 6 bits represent physical input (63=all, 62=VKB). If 4096 is not set, low 10 bits (0..1023) are input start channel (ReaRoute/Loopback start at 512). If 2048 is set, input is multichannel input (using track channel count), or if 1024 is set, input is stereo input, otherwise input is mono.
I_RECMODE : int * : record mode, 0=input, 1=stereo out, 2=none, 3=stereo out w/latency compensation, 4=midi output, 5=mono out, 6=mono out w/ latency compensation, 7=midi overdub, 8=midi replace
I_RECMODE_FLAGS : int * : record mode flags, &3=output recording mode (0=post fader, 1=pre-fx, 2=post-fx/pre-fader)
I_RECMON : int * : record monitoring, 0=off, 1=normal, 2=not when playing (tape style)
I_RECMONITEMS : int * : monitor items while recording, 0=off, 1=on
B_AUTO_RECARM : bool * : automatically set record arm when selected (does not immediately affect recarm state, script should set directly if desired)
I_VUMODE : int * : track vu mode, &1:disabled, &30==0:stereo peaks, &30==2:multichannel peaks, &30==4:stereo RMS, &30==8:combined RMS, &30==12:LUFS-M, &30==16:LUFS-S (readout=max), &30==20:LUFS-S (readout=current), &32:LUFS calculation on channels 1+2 only
I_AUTOMODE : int * : track automation mode, 0=trim/off, 1=read, 2=touch, 3=write, 4=latch
I_NCHAN : int * : number of track channels, 2-128, even numbers only
I_SELECTED : int * : track selected, 0=unselected, 1=selected
I_WNDH : int * : current TCP window height in pixels including envelopes (read-only)
I_TCPH : int * : current TCP window height in pixels not including envelopes (read-only)
I_TCPY : int * : current TCP window Y-position in pixels relative to top of arrange view (read-only)
I_MCPX : int * : current MCP X-position in pixels relative to mixer container (read-only)
I_MCPY : int * : current MCP Y-position in pixels relative to mixer container (read-only)
I_MCPW : int * : current MCP width in pixels (read-only)
I_MCPH : int * : current MCP height in pixels (read-only)
I_FOLDERDEPTH : int * : folder depth change, 0=normal, 1=track is a folder parent, -1=track is the last in the innermost folder, -2=track is the last in the innermost and next-innermost folders, etc
I_FOLDERCOMPACT : int * : folder collapsed state (only valid on folders), 0=normal, 1=collapsed, 2=fully collapsed
I_MIDIHWOUT : int * : track midi hardware output index, <0=disabled, low 5 bits are which channels (0=all, 1-16), next 5 bits are output device index (0-31)
I_MIDI_INPUT_CHANMAP : int * : -1 maps to source channel, otherwise 1-16 to map to MIDI channel
I_MIDI_CTL_CHAN : int * : -1 no link, 0-15 link to MIDI volume/pan on channel, 16 link to MIDI volume/pan on all channels
I_MIDI_TRACKSEL_FLAG : int * : MIDI editor track list options: &1=expand media items, &2=exclude from list, &4=auto-pruned
I_PERFFLAGS : int * : track performance flags, &1=no media buffering, &2=no anticipative FX
I_CUSTOMCOLOR : int * : custom color, OS dependent color|0x1000000 (i.e. ColorToNative(r,g,b)|0x1000000). If you do not |0x1000000, then it will not be used, but will store the color
I_HEIGHTOVERRIDE : int * : custom height override for TCP window, 0 for none, otherwise size in pixels
I_SPACER : int * : 1=TCP track spacer above this trackB_HEIGHTLOCK : bool * : track height lock (must set I_HEIGHTOVERRIDE before locking)
D_VOL : double * : trim volume of track, 0=-inf, 0.5=-6dB, 1=+0dB, 2=+6dB, etc
D_PAN : double * : trim pan of track, -1..1
D_WIDTH : double * : width of track, -1..1
D_DUALPANL : double * : dualpan position 1, -1..1, only if I_PANMODE==6
D_DUALPANR : double * : dualpan position 2, -1..1, only if I_PANMODE==6
I_PANMODE : int * : pan mode, 0=classic 3.x, 3=new balance, 5=stereo pan, 6=dual pan
D_PANLAW : double * : pan law of track, <0=project default, 0.5=-6dB, 0.707..=-3dB, 1=+0dB, 1.414..=-3dB with gain compensation, 2=-6dB with gain compensation, etc
I_PANLAW_FLAGS : int * : pan law flags, 0=sine taper, 1=hybrid taper with deprecated behavior when gain compensation enabled, 2=linear taper, 3=hybrid taper
P_ENV:<envchunkname or P_ENV:{GUID... : TrackEnvelope * : (read-only) chunkname can be <VOLENV, <PANENV, etc; GUID is the stringified envelope GUID.
B_SHOWINMIXER : bool * : track control panel visible in mixer (do not use on master track)
B_SHOWINTCP : bool * : track control panel visible in arrange view (do not use on master track)
B_MAINSEND : bool * : track sends audio to parent
C_MAINSEND_OFFS : char * : channel offset of track send to parent
C_MAINSEND_NCH : char * : channel count of track send to parent (0=use all child track channels, 1=use one channel only)
I_FREEMODE : int * : 1=track free item positioning enabled, 2=track fixed lanes enabled (call UpdateTimeline() after changing)
I_NUMFIXEDLANES : int * : number of track fixed lanes (fine to call with setNewValue, but returned value is read-only)
C_LANESCOLLAPSED : char * : fixed lane collapse state (1=lanes collapsed, 2=track displays as non-fixed-lanes but hidden lanes exist)
C_LANESETTINGS : char * : fixed lane settings (&1=auto-remove empty lanes at bottom, &2=do not auto-comp new recording, &4=newly recorded lanes play exclusively (else add lanes in layers), &8=big lanes (else small lanes), &16=add new recording at bottom (else record into first available lane), &32=hide lane buttons
C_LANEPLAYS:N : char * : on fixed lane tracks, 0=lane N does not play, 1=lane N plays exclusively, 2=lane N plays and other lanes also play (fine to call with setNewValue, but returned value is read-only)
C_ALLLANESPLAY : char * : on fixed lane tracks, 0=no lanes play, 1=all lanes play, 2=some lanes play (fine to call with setNewValue 0 or 1, but returned value is read-only)
C_BEATATTACHMODE : char * : track timebase, -1=project default, 0=time, 1=beats (position, length, rate), 2=beats (position only)
F_MCP_FXSEND_SCALE : float * : scale of fx+send area in MCP (0=minimum allowed, 1=maximum allowed)
F_MCP_FXPARM_SCALE : float * : scale of fx parameter area in MCP (0=minimum allowed, 1=maximum allowed)
F_MCP_SENDRGN_SCALE : float * : scale of send area as proportion of the fx+send total area (0=minimum allowed, 1=maximum allowed)
F_TCP_FXPARM_SCALE : float * : scale of TCP parameter area when TCP FX are embedded (0=min allowed, default, 1=max allowed)
I_PLAY_OFFSET_FLAG : int * : track media playback offset state, &1=bypassed, &2=offset value is measured in samples (otherwise measured in seconds)
D_PLAY_OFFSET : double * : track media playback offset, units depend on I_PLAY_OFFSET_FLAG
## SetMIDIEditorGrid
```
reaper.SetMIDIEditorGrid(ReaProject project, number division)
```

Set the MIDI editor grid division. 0.25=quarter note, 1.0/3.0=half note tripet, etc.
## SetMixerScroll
```
MediaTrack reaper.SetMixerScroll(MediaTrack leftmosttrack)
```

Scroll the mixer so that leftmosttrack is the leftmost visible track. Returns the leftmost track after scrolling, which may be different from the passed-in track if there are not enough tracks to its right.
## SetMouseModifier
```
reaper.SetMouseModifier(string context, integer modifier_flag, string action)
```

Set the mouse modifier assignment for a specific modifier key assignment, in a specific context.
Context is a string like "MM_CTX_ITEM" (see reaper-mouse.ini) or "Media item left drag" (unlocalized).
Modifier flag is a number from 0 to 15: add 1 for shift, 2 for control, 4 for alt, 8 for win.
(macOS: add 1 for shift, 2 for command, 4 for opt, 8 for control.)
For left-click and double-click contexts, the action can be any built-in command ID number
or any custom action ID string. Find built-in command IDs in the REAPER actions window
(enable "show command IDs" in the context menu), and find custom action ID strings in reaper-kb.ini.
The action string may be a mouse modifier ID (see reaper-mouse.ini) with " m" appended to it,
or (for click/double-click contexts) a command ID with " c" appended to it,
or the text that appears in the mouse modifiers preferences dialog, like "Move item" (unlocalized).
For example, SetMouseModifier("MM_CTX_ITEM", 0, "1 m") and SetMouseModifier("Media item left drag", 0, "Move item") are equivalent.
SetMouseModifier(context, modifier_flag, -1) will reset that mouse modifier to default.
SetMouseModifier(context, -1, -1) will reset the entire context to default.
SetMouseModifier(-1, -1, -1) will reset all contexts to default.
See GetMouseModifier.
## SetOnlyTrackSelected
```
reaper.SetOnlyTrackSelected(MediaTrack track)
```

Set exactly one track selected, deselect all others
## SetProjectGrid
```
reaper.SetProjectGrid(ReaProject project, number division)
```

Set the arrange view grid division. 0.25=quarter note, 1.0/3.0=half note triplet, etc.
## SetProjectMarker
```
boolean reaper.SetProjectMarker(integer markrgnindexnumber, boolean isrgn, number pos, number rgnend, string name)
```

Note: this function can't clear a marker's name (an empty string will leave the name unchanged), see SetProjectMarker4.
## SetProjectMarker2
```
boolean reaper.SetProjectMarker2(ReaProject proj, integer markrgnindexnumber, boolean isrgn, number pos, number rgnend, string name)
```

Note: this function can't clear a marker's name (an empty string will leave the name unchanged), see SetProjectMarker4.
## SetProjectMarker3
```
boolean reaper.SetProjectMarker3(ReaProject proj, integer markrgnindexnumber, boolean isrgn, number pos, number rgnend, string name, integer color)
```

Note: this function can't clear a marker's name (an empty string will leave the name unchanged), see SetProjectMarker4.
## SetProjectMarker4
```
boolean reaper.SetProjectMarker4(ReaProject proj, integer markrgnindexnumber, boolean isrgn, number pos, number rgnend, string name, integer color, integer flags)
```

color should be 0 to not change, or ColorToNative(r,g,b)|0x1000000, flags&1 to clear name
## SetProjectMarkerByIndex
```
boolean reaper.SetProjectMarkerByIndex(ReaProject proj, integer markrgnidx, boolean isrgn, number pos, number rgnend, integer IDnumber, string name, integer color)
```

See SetProjectMarkerByIndex2.
## SetProjectMarkerByIndex2
```
boolean reaper.SetProjectMarkerByIndex2(ReaProject proj, integer markrgnidx, boolean isrgn, number pos, number rgnend, integer IDnumber, string name, integer color, integer flags)
```

Differs from SetProjectMarker4 in that markrgnidx is 0 for the first marker/region, 1 for the next, etc (see EnumProjectMarkers3), rather than representing the displayed marker/region ID number (see SetProjectMarker3). IDnumber < 0 to ignore. Function will fail if attempting to set a duplicate ID number for a region (duplicate ID numbers for markers are OK). flags&1 to clear name. If flags&2, markers will not be re-sorted, and after making updates, you MUST call SetProjectMarkerByIndex2 with markrgnidx=-1 and flags&2 to force re-sort/UI updates.
## SetProjExtState
```
integer reaper.SetProjExtState(ReaProject proj, string extname, string key, string value)
```

Save a key/value pair for a specific extension, to be restored the next time this specific project is loaded. Typically extname will be the name of a reascript or extension section. If key is NULL or "", all extended data for that extname will be deleted. If val is NULL or "", the data previously associated with that key will be deleted. Returns the size of the state for this extname. See GetProjExtState, EnumProjExtState.
## SetRegionRenderMatrix
```
reaper.SetRegionRenderMatrix(ReaProject proj, integer regionindex, MediaTrack track, integer flag)
```

Add (flag > 0) or remove (flag < 0) a track from this region when using the region render matrix. If adding, flag==2 means force mono, flag==4 means force stereo, flag==N means force N/2 channels.
## SetTakeMarker
```
integer reaper.SetTakeMarker(MediaItem_Take take, integer idx, string nameIn, optional number srcposIn, optional integer colorIn)
```

Inserts or updates a take marker. If idx<0, a take marker will be added, otherwise an existing take marker will be updated. Returns the index of the new or updated take marker (which may change if srcPos is updated). See GetNumTakeMarkers, GetTakeMarker, DeleteTakeMarker
## SetTakeStretchMarker
```
integer reaper.SetTakeStretchMarker(MediaItem_Take take, integer idx, number pos, optional number srcposIn)
```

Adds or updates a stretch marker. If idx<0, stretch marker will be added. If idx>=0, stretch marker will be updated. When adding, if srcposInOptional is omitted, source position will be auto-calculated. When updating a stretch marker, if srcposInOptional is omitted, srcpos will not be modified. Position/srcposition values will be constrained to nearby stretch markers. Returns index of stretch marker, or -1 if did not insert (or marker already existed at time).
## SetTakeStretchMarkerSlope
```
boolean reaper.SetTakeStretchMarkerSlope(MediaItem_Take take, integer idx, number slope)
```

See GetTakeStretchMarkerSlope
## SetTempoTimeSigMarker
```
boolean reaper.SetTempoTimeSigMarker(ReaProject proj, integer ptidx, number timepos, integer measurepos, number beatpos, number bpm, integer timesig_num, integer timesig_denom, boolean lineartempo)
```

Set parameters of a tempo/time signature marker. Provide either timepos (with measurepos=-1, beatpos=-1), or measurepos and beatpos (with timepos=-1). If timesig_num and timesig_denom are zero, the previous time signature will be used. ptidx=-1 will insert a new tempo/time signature marker. See CountTempoTimeSigMarkers, GetTempoTimeSigMarker, AddTempoTimeSigMarker.
## SetThemeColor
```
integer reaper.SetThemeColor(string ini_key, integer color, integer flags)
```

Temporarily updates the theme color to the color specified (or the theme default color if -1 is specified). Returns -1 on failure, otherwise returns the color (or transformed-color). Note that the UI is not updated by this, the caller should call UpdateArrange() etc as necessary. If the low bit of flags is set, any color transformations are bypassed. To read a value see GetThemeColor.Currently valid ini_keys:
## SetToggleCommandState
```
boolean reaper.SetToggleCommandState(integer section_id, integer command_id, integer state)
```

Updates the toggle state of an action, returns true if succeeded. Only ReaScripts can have their toggle states changed programmatically. See RefreshToolbar2.
## SetTrackAutomationMode
```
reaper.SetTrackAutomationMode(MediaTrack tr, integer mode)
```

No description available.
## SetTrackColor
```
reaper.SetTrackColor(MediaTrack track, integer color)
```

Set the custom track color, color is OS dependent (i.e. ColorToNative(r,g,b). To unset the track color, see SetMediaTrackInfo_Value I_CUSTOMCOLOR
## SetTrackMIDILyrics
```
boolean reaper.SetTrackMIDILyrics(MediaTrack track, integer flag, string str)
```

Set all MIDI lyrics on the track. Lyrics will be stuffed into any MIDI items found in range. Flag is unused at present. str is passed in as beat position, tab, text, tab (example with flag=2: "1.1.2\tLyric for measure 1 beat 2\t2.1.1\tLyric for measure 2 beat 1	"). See GetTrackMIDILyrics
## SetTrackMIDINoteName
```
boolean reaper.SetTrackMIDINoteName(integer track, integer pitch, integer chan, string name)
```

channel < 0 assigns these note names to all channels.
## SetTrackMIDINoteNameEx
```
boolean reaper.SetTrackMIDINoteNameEx(ReaProject proj, MediaTrack track, integer pitch, integer chan, string name)
```

channel < 0 assigns note name to all channels. pitch 128 assigns name for CC0, pitch 129 for CC1, etc.
## SetTrackSelected
```
reaper.SetTrackSelected(MediaTrack track, boolean selected)
```

No description available.
## SetTrackSendInfo_Value
```
boolean reaper.SetTrackSendInfo_Value(MediaTrack tr, integer category, integer sendidx, string parmname, number newvalue)
```

Set send/receive/hardware output numerical-value attributes, return true on success.
category is <0 for receives, 0=sends, >0 for hardware outputs
parameter names:
B_MUTE : bool *
B_PHASE : bool * : true to flip phase
B_MONO : bool *
D_VOL : double * : 1.0 = +0dB etc
D_PAN : double * : -1..+1
D_PANLAW : double * : 1.0=+0.0db, 0.5=-6dB, -1.0 = projdef etc
I_SENDMODE : int * : 0=post-fader, 1=pre-fx, 2=post-fx (deprecated), 3=post-fx
I_AUTOMODE : int * : automation mode (-1=use track automode, 0=trim/off, 1=read, 2=touch, 3=write, 4=latch)
I_SRCCHAN : int * : -1 for no audio send. Low 10 bits specify channel offset, and higher bits specify channel count. (srcchan>>10) == 0 for stereo, 1 for mono, 2 for 4 channel, 3 for 6 channel, etc.
I_DSTCHAN : int * : low 10 bits are destination index, &1024 set to mix to mono.
I_MIDIFLAGS : int * : low 5 bits=source channel 0=all, 1-16, 31=MIDI send disabled, next 5 bits=dest channel, 0=orig, 1-16=chan. &1024 for faders-send MIDI vol/pan. (>>14)&255 = src bus (0 for all, 1 for normal, 2+). (>>22)&255=destination bus (0 for all, 1 for normal, 2+)
See CreateTrackSend, RemoveTrackSend, GetTrackNumSends.
## SetTrackSendUIPan
```
boolean reaper.SetTrackSendUIPan(MediaTrack track, integer send_idx, number pan, integer isend)
```

send_idx<0 for receives, >=0 for hw ouputs, >=nb_of_hw_ouputs for sends. isend=1 for end of edit, -1 for an instant edit (such as reset), 0 for normal tweak.
## SetTrackSendUIVol
```
boolean reaper.SetTrackSendUIVol(MediaTrack track, integer send_idx, number vol, integer isend)
```

send_idx<0 for receives, >=0 for hw ouputs, >=nb_of_hw_ouputs for sends. isend=1 for end of edit, -1 for an instant edit (such as reset), 0 for normal tweak.
## SetTrackStateChunk
```
boolean reaper.SetTrackStateChunk(MediaTrack track, string str, boolean isundo)
```

Sets the RPPXML state of a track, returns true if successful. Undo flag is a performance/caching hint.
## SetTrackUIInputMonitor
```
integer reaper.SetTrackUIInputMonitor(MediaTrack track, integer monitor, integer igngroupflags)
```

monitor: 0=no monitoring, 1=monitoring, 2=auto-monitoring. returns new value or -1 if error. igngroupflags: &1 to prevent track grouping, &2 to prevent selection ganging
## SetTrackUIMute
```
integer reaper.SetTrackUIMute(MediaTrack track, integer mute, integer igngroupflags)
```

mute: <0 toggles, >0 sets mute, 0=unsets mute. returns new value or -1 if error. igngroupflags: &1 to prevent track grouping, &2 to prevent selection ganging
## SetTrackUIPan
```
number reaper.SetTrackUIPan(MediaTrack track, number pan, boolean relative, boolean done, integer igngroupflags)
```

igngroupflags: &1 to prevent track grouping, &2 to prevent selection ganging
## SetTrackUIPolarity
```
integer reaper.SetTrackUIPolarity(MediaTrack track, integer polarity, integer igngroupflags)
```

polarity (AKA phase): <0 toggles, 0=normal, >0=inverted. returns new value or -1 if error.igngroupflags: &1 to prevent track grouping, &2 to prevent selection ganging
## SetTrackUIRecArm
```
integer reaper.SetTrackUIRecArm(MediaTrack track, integer recarm, integer igngroupflags)
```

recarm: <0 toggles, >0 sets recarm, 0=unsets recarm. returns new value or -1 if error. igngroupflags: &1 to prevent track grouping, &2 to prevent selection ganging
## SetTrackUISolo
```
integer reaper.SetTrackUISolo(MediaTrack track, integer solo, integer igngroupflags)
```

solo: <0 toggles, 1 sets solo (default mode), 0=unsets solo, 2 sets solo (non-SIP), 4 sets solo (SIP). returns new value or -1 if error. igngroupflags: &1 to prevent track grouping, &2 to prevent selection ganging
## SetTrackUIVolume
```
number reaper.SetTrackUIVolume(MediaTrack track, number volume, boolean relative, boolean done, integer igngroupflags)
```

igngroupflags: &1 to prevent track grouping, &2 to prevent selection ganging
## SetTrackUIWidth
```
number reaper.SetTrackUIWidth(MediaTrack track, number width, boolean relative, boolean done, integer igngroupflags)
```

igngroupflags: &1 to prevent track grouping, &2 to prevent selection ganging
## ShowActionList
```
reaper.ShowActionList(KbdSectionInfo section, HWND callerWnd)
```

No description available.
## ShowConsoleMsg
```
reaper.ShowConsoleMsg(string msg)
```

Show a message to the user (also useful for debugging). Send "\n" for newline, "" to clear the console. Prefix string with "!SHOW:" and text will be added to console without opening the window. See ClearConsole
## ShowMessageBox
```
integer reaper.ShowMessageBox(string msg, string title, integer type)
```

type 0=OK,1=OKCANCEL,2=ABORTRETRYIGNORE,3=YESNOCANCEL,4=YESNO,5=RETRYCANCEL : ret 1=OK,2=CANCEL,3=ABORT,4=RETRY,5=IGNORE,6=YES,7=NO
## ShowPopupMenu
```
reaper.ShowPopupMenu(string name, integer x, integer y, HWND hwndParent, identifier ctx, integer ctx2, integer ctx3)
```

shows a context menu, valid names include: track_input, track_panel, track_area, track_routing, item, ruler, envelope, envelope_point, envelope_item. ctxOptional can be a track pointer for track_*, item pointer for item* (but is optional). for envelope_point, ctx2Optional has point index, ctx3Optional has item index (0=main envelope, 1=first AI). for envelope_item, ctx2Optional has AI index (1=first AI)
## SLIDER2DB
```
number reaper.SLIDER2DB(number y)
```

No description available.
## SnapToGrid
```
number reaper.SnapToGrid(ReaProject project, number time_pos)
```

No description available.
## SoloAllTracks
```
reaper.SoloAllTracks(integer solo)
```

solo=2 for SIP
## Splash_GetWnd
```
HWND reaper.Splash_GetWnd()
```

gets the splash window, in case you want to display a message over it. Returns NULL when the splash window is not displayed.
## SplitMediaItem
```
MediaItem reaper.SplitMediaItem(MediaItem item, number position)
```

the original item becomes the left-hand split, the function returns the right-hand split (or NULL if the split failed)
## stringToGuid
```
string gGUID = reaper.stringToGuid(string str, string gGUID)
```

No description available.
## StuffMIDIMessage
```
reaper.StuffMIDIMessage(integer mode, integer msg1, integer msg2, integer msg3)
```

Stuffs a 3 byte MIDI message into either the Virtual MIDI Keyboard queue, or the MIDI-as-control input queue, or sends to a MIDI hardware output. mode=0 for VKB, 1 for control (actions map etc), 2 for VKB-on-current-channel; 16 for external MIDI device 0, 17 for external MIDI device 1, etc; see GetNumMIDIOutputs, GetMIDIOutputName.
## TakeFX_AddByName
```
integer reaper.TakeFX_AddByName(MediaItem_Take take, string fxname, integer instantiate)
```

Adds or queries the position of a named FX in a take. See TrackFX_AddByName() for information on fxname and instantiate. FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_CopyToTake
```
reaper.TakeFX_CopyToTake(MediaItem_Take src_take, integer src_fx, MediaItem_Take dest_take, integer dest_fx, boolean is_move)
```

Copies (or moves) FX from src_take to dest_take. Can be used with src_take=dest_take to reorder. FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_CopyToTrack
```
reaper.TakeFX_CopyToTrack(MediaItem_Take src_take, integer src_fx, MediaTrack dest_track, integer dest_fx, boolean is_move)
```

Copies (or moves) FX from src_take to dest_track. dest_fx can have 0x1000000 set to reference input FX. FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_Delete
```
boolean reaper.TakeFX_Delete(MediaItem_Take take, integer fx)
```

Remove a FX from take chain (returns true on success) FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_EndParamEdit
```
boolean reaper.TakeFX_EndParamEdit(MediaItem_Take take, integer fx, integer param)
```

FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_FormatParamValue
```
boolean retval, string buf = reaper.TakeFX_FormatParamValue(MediaItem_Take take, integer fx, integer param, number val)
```

Note: only works with FX that support Cockos VST extensions. FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_FormatParamValueNormalized
```
boolean retval, string buf = reaper.TakeFX_FormatParamValueNormalized(MediaItem_Take take, integer fx, integer param, number value, string buf)
```

Note: only works with FX that support Cockos VST extensions. FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetChainVisible
```
integer reaper.TakeFX_GetChainVisible(MediaItem_Take take)
```

returns index of effect visible in chain, or -1 for chain hidden, or -2 for chain visible but no effect selected
## TakeFX_GetCount
```
integer reaper.TakeFX_GetCount(MediaItem_Take take)
```

No description available.
## TakeFX_GetEnabled
```
boolean reaper.TakeFX_GetEnabled(MediaItem_Take take, integer fx)
```

See TakeFX_SetEnabled FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetEnvelope
```
TrackEnvelope reaper.TakeFX_GetEnvelope(MediaItem_Take take, integer fxindex, integer parameterindex, boolean create)
```

Returns the FX parameter envelope. If the envelope does not exist and create=true, the envelope will be created. If the envelope already exists and is bypassed and create=true, then the envelope will be unbypassed. FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetFloatingWindow
```
HWND reaper.TakeFX_GetFloatingWindow(MediaItem_Take take, integer index)
```

returns HWND of floating window for effect index, if any FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetFormattedParamValue
```
boolean retval, string buf = reaper.TakeFX_GetFormattedParamValue(MediaItem_Take take, integer fx, integer param)
```

FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetFXGUID
```
string GUID = reaper.TakeFX_GetFXGUID(MediaItem_Take take, integer fx)
```

FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetFXName
```
boolean retval, string buf = reaper.TakeFX_GetFXName(MediaItem_Take take, integer fx)
```

FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetIOSize
```
integer retval, integer inputPins, integer outputPins = reaper.TakeFX_GetIOSize(MediaItem_Take take, integer fx)
```

Gets the number of input/output pins for FX if available, returns plug-in type or -1 on error FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetNamedConfigParm
```
boolean retval, string buf = reaper.TakeFX_GetNamedConfigParm(MediaItem_Take take, integer fx, string parmname)
```

gets plug-in specific named configuration value (returns true on success). see TrackFX_GetNamedConfigParm FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetNumParams
```
integer reaper.TakeFX_GetNumParams(MediaItem_Take take, integer fx)
```

FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetOffline
```
boolean reaper.TakeFX_GetOffline(MediaItem_Take take, integer fx)
```

See TakeFX_SetOffline FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetOpen
```
boolean reaper.TakeFX_GetOpen(MediaItem_Take take, integer fx)
```

Returns true if this FX UI is open in the FX chain window or a floating window. See TakeFX_SetOpen FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetParam
```
number retval, number minval, number maxval = reaper.TakeFX_GetParam(MediaItem_Take take, integer fx, integer param)
```

FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetParameterStepSizes
```
boolean retval, number step, number smallstep, number largestep, boolean istoggle = reaper.TakeFX_GetParameterStepSizes(MediaItem_Take take, integer fx, integer param)
```

FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetParamEx
```
number retval, number minval, number maxval, number midval = reaper.TakeFX_GetParamEx(MediaItem_Take take, integer fx, integer param)
```

FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetParamFromIdent
```
integer reaper.TakeFX_GetParamFromIdent(MediaItem_Take take, integer fx, string ident_str)
```

gets the parameter index from an identifying string (:wet, :bypass, or a string returned from GetParamIdent), or -1 if unknown. FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetParamIdent
```
boolean retval, string buf = reaper.TakeFX_GetParamIdent(MediaItem_Take take, integer fx, integer param)
```

gets an identifying string for the parameter FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetParamName
```
boolean retval, string buf = reaper.TakeFX_GetParamName(MediaItem_Take take, integer fx, integer param)
```

FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetParamNormalized
```
number reaper.TakeFX_GetParamNormalized(MediaItem_Take take, integer fx, integer param)
```

FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetPinMappings
```
integer retval, integer high32 = reaper.TakeFX_GetPinMappings(MediaItem_Take take, integer fx, integer isoutput, integer pin)
```

gets the effective channel mapping bitmask for a particular pin. high32Out will be set to the high 32 bits. Add 0x1000000 to pin index in order to access the second 64 bits of mappings independent of the first 64 bits. FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetPreset
```
boolean retval, string presetname = reaper.TakeFX_GetPreset(MediaItem_Take take, integer fx)
```

Get the name of the preset currently showing in the REAPER dropdown, or the full path to a factory preset file for VST3 plug-ins (.vstpreset). See TakeFX_SetPreset. FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetPresetIndex
```
integer retval, integer numberOfPresets = reaper.TakeFX_GetPresetIndex(MediaItem_Take take, integer fx)
```

Returns current preset index, or -1 if error. numberOfPresetsOut will be set to total number of presets available. See TakeFX_SetPresetByIndex FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_GetUserPresetFilename
```
string fn = reaper.TakeFX_GetUserPresetFilename(MediaItem_Take take, integer fx)
```

FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_NavigatePresets
```
boolean reaper.TakeFX_NavigatePresets(MediaItem_Take take, integer fx, integer presetmove)
```

presetmove==1 activates the next preset, presetmove==-1 activates the previous preset, etc. FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_SetEnabled
```
reaper.TakeFX_SetEnabled(MediaItem_Take take, integer fx, boolean enabled)
```

See TakeFX_GetEnabled FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_SetNamedConfigParm
```
boolean reaper.TakeFX_SetNamedConfigParm(MediaItem_Take take, integer fx, string parmname, string value)
```

gets plug-in specific named configuration value (returns true on success). see TrackFX_SetNamedConfigParm FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_SetOffline
```
reaper.TakeFX_SetOffline(MediaItem_Take take, integer fx, boolean offline)
```

See TakeFX_GetOffline FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_SetOpen
```
reaper.TakeFX_SetOpen(MediaItem_Take take, integer fx, boolean open)
```

Open this FX UI. See TakeFX_GetOpen FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_SetParam
```
boolean reaper.TakeFX_SetParam(MediaItem_Take take, integer fx, integer param, number val)
```

FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_SetParamNormalized
```
boolean reaper.TakeFX_SetParamNormalized(MediaItem_Take take, integer fx, integer param, number value)
```

FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_SetPinMappings
```
boolean reaper.TakeFX_SetPinMappings(MediaItem_Take take, integer fx, integer isoutput, integer pin, integer low32bits, integer hi32bits)
```

sets the channel mapping bitmask for a particular pin. returns false if unsupported (not all types of plug-ins support this capability). Add 0x1000000 to pin index in order to access the second 64 bits of mappings independent of the first 64 bits. FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_SetPreset
```
boolean reaper.TakeFX_SetPreset(MediaItem_Take take, integer fx, string presetname)
```

Activate a preset with the name shown in the REAPER dropdown. Full paths to .vstpreset files are also supported for VST3 plug-ins. See TakeFX_GetPreset. FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_SetPresetByIndex
```
boolean reaper.TakeFX_SetPresetByIndex(MediaItem_Take take, integer fx, integer idx)
```

Sets the preset idx, or the factory preset (idx==-2), or the default user preset (idx==-1). Returns true on success. See TakeFX_GetPresetIndex. FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeFX_Show
```
reaper.TakeFX_Show(MediaItem_Take take, integer index, integer showFlag)
```

showflag=0 for hidechain, =1 for show chain(index valid), =2 for hide floating window(index valid), =3 for show floating window (index valid) FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TakeIsMIDI
```
boolean reaper.TakeIsMIDI(MediaItem_Take take)
```

Returns true if the active take contains MIDI.
## ThemeLayout_GetLayout
```
boolean retval, string name = reaper.ThemeLayout_GetLayout(string section, integer idx)
```

Gets theme layout information. section can be 'global' for global layout override, 'seclist' to enumerate a list of layout sections, otherwise a layout section such as 'mcp', 'tcp', 'trans', etc. idx can be -1 to query the current value, -2 to get the description of the section (if not global), -3 will return the current context DPI-scaling (256=normal, 512=retina, etc), or 0..x. returns false if failed.
## ThemeLayout_GetParameter
```
string retval, optional string desc, optional integer value, optional integer defValue, optional integer minValue, optional integer maxValue = reaper.ThemeLayout_GetParameter(integer wp)
```

returns theme layout parameter. return value is cfg-name, or nil/empty if out of range.
## ThemeLayout_RefreshAll
```
reaper.ThemeLayout_RefreshAll()
```

Refreshes all layouts
## ThemeLayout_SetLayout
```
boolean reaper.ThemeLayout_SetLayout(string section, string layout)
```

Sets theme layout override for a particular section -- section can be 'global' or 'mcp' etc. If setting global layout, prefix a ! to the layout string to clear any per-layout overrides. Returns false if failed.
## ThemeLayout_SetParameter
```
boolean reaper.ThemeLayout_SetParameter(integer wp, integer value, boolean persist)
```

sets theme layout parameter to value. persist=true in order to have change loaded on next theme load. note that the caller should update layouts via ??? to make changes visible.
## time_precise
```
number reaper.time_precise()
```

Gets a precise system timestamp in seconds
## TimeMap2_beatsToTime
```
number reaper.TimeMap2_beatsToTime(ReaProject proj, number tpos, optional integer measuresIn)
```

convert a beat position (or optionally a beats+measures if measures is non-NULL) to time.
## TimeMap2_GetDividedBpmAtTime
```
number reaper.TimeMap2_GetDividedBpmAtTime(ReaProject proj, number time)
```

get the effective BPM at the time (seconds) position (i.e. 2x in /8 signatures)
## TimeMap2_GetNextChangeTime
```
number reaper.TimeMap2_GetNextChangeTime(ReaProject proj, number time)
```

when does the next time map (tempo or time sig) change occur
## TimeMap2_QNToTime
```
number reaper.TimeMap2_QNToTime(ReaProject proj, number qn)
```

converts project QN position to time.
## TimeMap2_timeToBeats
```
number retval, optional integer measures, optional integer cml, optional number fullbeats, optional integer cdenom = reaper.TimeMap2_timeToBeats(ReaProject proj, number tpos)
```

convert a time into beats.
if measures is non-NULL, measures will be set to the measure count, return value will be beats since measure.
if cml is non-NULL, will be set to current measure length in beats (i.e. time signature numerator)
if fullbeats is non-NULL, and measures is non-NULL, fullbeats will get the full beat count (same value returned if measures is NULL).
if cdenom is non-NULL, will be set to the current time signature denominator.
## TimeMap2_timeToQN
```
number reaper.TimeMap2_timeToQN(ReaProject proj, number tpos)
```

converts project time position to QN position.
## TimeMap_curFrameRate
```
number retval, boolean dropFrame = reaper.TimeMap_curFrameRate(ReaProject proj)
```

Gets project framerate, and optionally whether it is drop-frame timecode
## TimeMap_GetDividedBpmAtTime
```
number reaper.TimeMap_GetDividedBpmAtTime(number time)
```

get the effective BPM at the time (seconds) position (i.e. 2x in /8 signatures)
## TimeMap_GetMeasureInfo
```
number retval, number qn_start, number qn_end, integer timesig_num, integer timesig_denom, number tempo = reaper.TimeMap_GetMeasureInfo(ReaProject proj, integer measure)
```

Get the QN position and time signature information for the start of a measure. Return the time in seconds of the measure start.
## TimeMap_GetMetronomePattern
```
integer retval, string pattern = reaper.TimeMap_GetMetronomePattern(ReaProject proj, number time, string pattern)
```

Fills in a string representing the active metronome pattern. For example, in a 7/8 measure divided 3+4, the pattern might be "ABCABCD". For backwards compatibility, by default the function will return 1 for each primary beat and 2 for each non-primary beat, so "1221222" in this example, and does not support triplets. If buf is set to "EXTENDED", the function will return the full string as displayed in the pattern editor, including all beat types and triplet representations. Pass in "SET:string" with a correctly formed pattern string matching the current time signature numerator to set the click pattern. The time signature numerator can be deduced from the returned string, and the function returns the time signature denominator.
## TimeMap_GetTimeSigAtTime
```
integer timesig_num, integer timesig_denom, number tempo = reaper.TimeMap_GetTimeSigAtTime(ReaProject proj, number time)
```

get the effective time signature and tempo
## TimeMap_QNToMeasures
```
integer retval, optional number qnMeasureStart, optional number qnMeasureEnd = reaper.TimeMap_QNToMeasures(ReaProject proj, number qn)
```

Find which measure the given QN position falls in.
## TimeMap_QNToTime
```
number reaper.TimeMap_QNToTime(number qn)
```

converts project QN position to time.
## TimeMap_QNToTime_abs
```
number reaper.TimeMap_QNToTime_abs(ReaProject proj, number qn)
```

Converts project quarter note count (QN) to time. QN is counted from the start of the project, regardless of any partial measures. See TimeMap2_QNToTime
## TimeMap_timeToQN
```
number reaper.TimeMap_timeToQN(number tpos)
```

converts project QN position to time.
## TimeMap_timeToQN_abs
```
number reaper.TimeMap_timeToQN_abs(ReaProject proj, number tpos)
```

Converts project time position to quarter note count (QN). QN is counted from the start of the project, regardless of any partial measures. See TimeMap2_timeToQN
## ToggleTrackSendUIMute
```
boolean reaper.ToggleTrackSendUIMute(MediaTrack track, integer send_idx)
```

send_idx<0 for receives, >=0 for hw ouputs, >=nb_of_hw_ouputs for sends.
## Track_GetPeakHoldDB
```
number reaper.Track_GetPeakHoldDB(MediaTrack track, integer channel, boolean clear)
```

Returns meter hold state, in dB*0.01 (0 = +0dB, -0.01 = -1dB, 0.02 = +2dB, etc). If clear is set, clears the meter hold. If channel==1024 or channel==1025, returns loudness values if this is the master track or this track's VU meters are set to display loudness.
## Track_GetPeakInfo
```
number reaper.Track_GetPeakInfo(MediaTrack track, integer channel)
```

Returns peak meter value (1.0=+0dB, 0.0=-inf) for channel. If channel==1024 or channel==1025, returns loudness values if this is the master track or this track's VU meters are set to display loudness.
## TrackCtl_SetToolTip
```
reaper.TrackCtl_SetToolTip(string fmt, integer xpos, integer ypos, boolean topmost)
```

displays tooltip at location, or removes if empty string
## TrackFX_AddByName
```
integer reaper.TrackFX_AddByName(MediaTrack track, string fxname, boolean recFX, integer instantiate)
```

Adds or queries the position of a named FX from the track FX chain (recFX=false) or record input FX/monitoring FX (recFX=true, monitoring FX are on master track). Specify a negative value for instantiate to always create a new effect, 0 to only query the first instance of an effect, or a positive value to add an instance if one is not found. If instantiate is <= -1000, it is used for the insertion position (-1000 is first item in chain, -1001 is second, etc). fxname can have prefix to specify type: VST3:,VST2:,VST:,AU:,JS:, or DX:, or FXADD: which adds selected items from the currently-open FX browser, FXADD:2 to limit to 2 FX added, or FXADD:2e to only succeed if exactly 2 FX are selected. Returns -1 on failure or the new position in chain on success. FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_CopyToTake
```
reaper.TrackFX_CopyToTake(MediaTrack src_track, integer src_fx, MediaItem_Take dest_take, integer dest_fx, boolean is_move)
```

Copies (or moves) FX from src_track to dest_take. src_fx can have 0x1000000 set to reference input FX. FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_CopyToTrack
```
reaper.TrackFX_CopyToTrack(MediaTrack src_track, integer src_fx, MediaTrack dest_track, integer dest_fx, boolean is_move)
```

Copies (or moves) FX from src_track to dest_track. Can be used with src_track=dest_track to reorder, FX indices have 0x1000000 set to reference input FX. FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_Delete
```
boolean reaper.TrackFX_Delete(MediaTrack track, integer fx)
```

Remove a FX from track chain (returns true on success) FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_EndParamEdit
```
boolean reaper.TrackFX_EndParamEdit(MediaTrack track, integer fx, integer param)
```

FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_FormatParamValue
```
boolean retval, string buf = reaper.TrackFX_FormatParamValue(MediaTrack track, integer fx, integer param, number val)
```

Note: only works with FX that support Cockos VST extensions. FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_FormatParamValueNormalized
```
boolean retval, string buf = reaper.TrackFX_FormatParamValueNormalized(MediaTrack track, integer fx, integer param, number value, string buf)
```

Note: only works with FX that support Cockos VST extensions. FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetByName
```
integer reaper.TrackFX_GetByName(MediaTrack track, string fxname, boolean instantiate)
```

Get the index of the first track FX insert that matches fxname. If the FX is not in the chain and instantiate is true, it will be inserted. See TrackFX_GetInstrument, TrackFX_GetEQ. Deprecated in favor of TrackFX_AddByName.
## TrackFX_GetChainVisible
```
integer reaper.TrackFX_GetChainVisible(MediaTrack track)
```

returns index of effect visible in chain, or -1 for chain hidden, or -2 for chain visible but no effect selected
## TrackFX_GetCount
```
integer reaper.TrackFX_GetCount(MediaTrack track)
```

No description available.
## TrackFX_GetEnabled
```
boolean reaper.TrackFX_GetEnabled(MediaTrack track, integer fx)
```

See TrackFX_SetEnabled FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetEQ
```
integer reaper.TrackFX_GetEQ(MediaTrack track, boolean instantiate)
```

Get the index of ReaEQ in the track FX chain. If ReaEQ is not in the chain and instantiate is true, it will be inserted. See TrackFX_GetInstrument, TrackFX_GetByName.
## TrackFX_GetEQBandEnabled
```
boolean reaper.TrackFX_GetEQBandEnabled(MediaTrack track, integer fxidx, integer bandtype, integer bandidx)
```

Returns true if the EQ band is enabled.
Returns false if the band is disabled, or if track/fxidx is not ReaEQ.
Bandtype: -1=master gain, 0=hipass, 1=loshelf, 2=band, 3=notch, 4=hishelf, 5=lopass, 6=bandpass, 7=parallel bandpass.
Bandidx (ignored for master gain): 0=target first band matching bandtype, 1=target 2nd band matching bandtype, etc.
## TrackFX_GetEQParam
```
boolean retval, integer bandtype, integer bandidx, integer paramtype, number normval = reaper.TrackFX_GetEQParam(MediaTrack track, integer fxidx, integer paramidx)
```

Returns false if track/fxidx is not ReaEQ.
Bandtype: -1=master gain, 0=hipass, 1=loshelf, 2=band, 3=notch, 4=hishelf, 5=lopass, 6=bandpass, 7=parallel bandpass.
Bandidx (ignored for master gain): 0=target first band matching bandtype, 1=target 2nd band matching bandtype, etc.
Paramtype (ignored for master gain): 0=freq, 1=gain, 2=Q.
See TrackFX_GetEQ, TrackFX_SetEQParam, TrackFX_GetEQBandEnabled, TrackFX_SetEQBandEnabled. FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetFloatingWindow
```
HWND reaper.TrackFX_GetFloatingWindow(MediaTrack track, integer index)
```

returns HWND of floating window for effect index, if any FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetFormattedParamValue
```
boolean retval, string buf = reaper.TrackFX_GetFormattedParamValue(MediaTrack track, integer fx, integer param)
```

FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetFXGUID
```
string GUID = reaper.TrackFX_GetFXGUID(MediaTrack track, integer fx)
```

FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetFXName
```
boolean retval, string buf = reaper.TrackFX_GetFXName(MediaTrack track, integer fx)
```

FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetInstrument
```
integer reaper.TrackFX_GetInstrument(MediaTrack track)
```

Get the index of the first track FX insert that is a virtual instrument, or -1 if none. See TrackFX_GetEQ, TrackFX_GetByName.
## TrackFX_GetIOSize
```
integer retval, integer inputPins, integer outputPins = reaper.TrackFX_GetIOSize(MediaTrack track, integer fx)
```

Gets the number of input/output pins for FX if available, returns plug-in type or -1 on error FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetNamedConfigParm
```
boolean retval, string buf = reaper.TrackFX_GetNamedConfigParm(MediaTrack track, integer fx, string parmname)
```

gets plug-in specific named configuration value (returns true on success).
## TrackFX_GetNumParams
```
integer reaper.TrackFX_GetNumParams(MediaTrack track, integer fx)
```

FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetOffline
```
boolean reaper.TrackFX_GetOffline(MediaTrack track, integer fx)
```

See TrackFX_SetOffline FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetOpen
```
boolean reaper.TrackFX_GetOpen(MediaTrack track, integer fx)
```

Returns true if this FX UI is open in the FX chain window or a floating window. See TrackFX_SetOpen FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetParam
```
number retval, number minval, number maxval = reaper.TrackFX_GetParam(MediaTrack track, integer fx, integer param)
```

FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetParameterStepSizes
```
boolean retval, number step, number smallstep, number largestep, boolean istoggle = reaper.TrackFX_GetParameterStepSizes(MediaTrack track, integer fx, integer param)
```

FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetParamEx
```
number retval, number minval, number maxval, number midval = reaper.TrackFX_GetParamEx(MediaTrack track, integer fx, integer param)
```

FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetParamFromIdent
```
integer reaper.TrackFX_GetParamFromIdent(MediaTrack track, integer fx, string ident_str)
```

gets the parameter index from an identifying string (:wet, :bypass, :delta, or a string returned from GetParamIdent), or -1 if unknown. FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetParamIdent
```
boolean retval, string buf = reaper.TrackFX_GetParamIdent(MediaTrack track, integer fx, integer param)
```

gets an identifying string for the parameter FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetParamName
```
boolean retval, string buf = reaper.TrackFX_GetParamName(MediaTrack track, integer fx, integer param)
```

FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetParamNormalized
```
number reaper.TrackFX_GetParamNormalized(MediaTrack track, integer fx, integer param)
```

FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetPinMappings
```
integer retval, integer high32 = reaper.TrackFX_GetPinMappings(MediaTrack tr, integer fx, integer isoutput, integer pin)
```

gets the effective channel mapping bitmask for a particular pin. high32Out will be set to the high 32 bits. Add 0x1000000 to pin index in order to access the second 64 bits of mappings independent of the first 64 bits. FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetPreset
```
boolean retval, string presetname = reaper.TrackFX_GetPreset(MediaTrack track, integer fx)
```

Get the name of the preset currently showing in the REAPER dropdown, or the full path to a factory preset file for VST3 plug-ins (.vstpreset). See TrackFX_SetPreset. FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetPresetIndex
```
integer retval, integer numberOfPresets = reaper.TrackFX_GetPresetIndex(MediaTrack track, integer fx)
```

Returns current preset index, or -1 if error. numberOfPresetsOut will be set to total number of presets available. See TrackFX_SetPresetByIndex FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_GetRecChainVisible
```
integer reaper.TrackFX_GetRecChainVisible(MediaTrack track)
```

returns index of effect visible in record input chain, or -1 for chain hidden, or -2 for chain visible but no effect selected
## TrackFX_GetRecCount
```
integer reaper.TrackFX_GetRecCount(MediaTrack track)
```

returns count of record input FX. To access record input FX, use a FX indices [0x1000000..0x1000000+n). On the master track, this accesses monitoring FX rather than record input FX.
## TrackFX_GetUserPresetFilename
```
string fn = reaper.TrackFX_GetUserPresetFilename(MediaTrack track, integer fx)
```

FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_NavigatePresets
```
boolean reaper.TrackFX_NavigatePresets(MediaTrack track, integer fx, integer presetmove)
```

presetmove==1 activates the next preset, presetmove==-1 activates the previous preset, etc. FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_SetEnabled
```
reaper.TrackFX_SetEnabled(MediaTrack track, integer fx, boolean enabled)
```

See TrackFX_GetEnabled FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_SetEQBandEnabled
```
boolean reaper.TrackFX_SetEQBandEnabled(MediaTrack track, integer fxidx, integer bandtype, integer bandidx, boolean enable)
```

Enable or disable a ReaEQ band.
Returns false if track/fxidx is not ReaEQ.
Bandtype: -1=master gain, 0=hipass, 1=loshelf, 2=band, 3=notch, 4=hishelf, 5=lopass, 6=bandpass, 7=parallel bandpass.
Bandidx (ignored for master gain): 0=target first band matching bandtype, 1=target 2nd band matching bandtype, etc.
## TrackFX_SetEQParam
```
boolean reaper.TrackFX_SetEQParam(MediaTrack track, integer fxidx, integer bandtype, integer bandidx, integer paramtype, number val, boolean isnorm)
```

Returns false if track/fxidx is not ReaEQ. Targets a band matching bandtype.
Bandtype: -1=master gain, 0=hipass, 1=loshelf, 2=band, 3=notch, 4=hishelf, 5=lopass, 6=bandpass, 7=parallel bandpass.
Bandidx (ignored for master gain): 0=target first band matching bandtype, 1=target 2nd band matching bandtype, etc.
Paramtype (ignored for master gain): 0=freq, 1=gain, 2=Q.
See TrackFX_GetEQ, TrackFX_GetEQParam, TrackFX_GetEQBandEnabled, TrackFX_SetEQBandEnabled. FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_SetNamedConfigParm
```
boolean reaper.TrackFX_SetNamedConfigParm(MediaTrack track, integer fx, string parmname, string value)
```

sets plug-in specific named configuration value (returns true on success).
## TrackFX_SetOffline
```
reaper.TrackFX_SetOffline(MediaTrack track, integer fx, boolean offline)
```

See TrackFX_GetOffline FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_SetOpen
```
reaper.TrackFX_SetOpen(MediaTrack track, integer fx, boolean open)
```

Open this FX UI. See TrackFX_GetOpen FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_SetParam
```
boolean reaper.TrackFX_SetParam(MediaTrack track, integer fx, integer param, number val)
```

FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_SetParamNormalized
```
boolean reaper.TrackFX_SetParamNormalized(MediaTrack track, integer fx, integer param, number value)
```

FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_SetPinMappings
```
boolean reaper.TrackFX_SetPinMappings(MediaTrack tr, integer fx, integer isoutput, integer pin, integer low32bits, integer hi32bits)
```

sets the channel mapping bitmask for a particular pin. returns false if unsupported (not all types of plug-ins support this capability). Add 0x1000000 to pin index in order to access the second 64 bits of mappings independent of the first 64 bits. FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_SetPreset
```
boolean reaper.TrackFX_SetPreset(MediaTrack track, integer fx, string presetname)
```

Activate a preset with the name shown in the REAPER dropdown. Full paths to .vstpreset files are also supported for VST3 plug-ins. See TrackFX_GetPreset. FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_SetPresetByIndex
```
boolean reaper.TrackFX_SetPresetByIndex(MediaTrack track, integer fx, integer idx)
```

Sets the preset idx, or the factory preset (idx==-2), or the default user preset (idx==-1). Returns true on success. See TrackFX_GetPresetIndex. FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackFX_Show
```
reaper.TrackFX_Show(MediaTrack track, integer index, integer showFlag)
```

showflag=0 for hidechain, =1 for show chain(index valid), =2 for hide floating window(index valid), =3 for show floating window (index valid) FX indices for tracks can have 0x1000000 added to them in order to reference record input FX (normal tracks) or hardware output FX (master track). FX indices can have 0x2000000 added to them, in which case they will be used to address FX in containers. To address a container, the 1-based subitem is multiplied by one plus the count of the FX chain and added to the 1-based container item index. e.g. to address the third item in the container at the second position of the track FX chain for tr, the index would be 0x2000000 + 3*(TrackFX_GetCount(tr)+1) + 2. This can be extended to sub-containers using TrackFX_GetNamedConfigParm with container_count and similar logic. In REAPER v7.06+, you can use the much more convenient method to navigate hierarchies, see TrackFX_GetNamedConfigParm with parent_container and container_item.X.
## TrackList_AdjustWindows
```
reaper.TrackList_AdjustWindows(boolean isMinor)
```

No description available.
## TrackList_UpdateAllExternalSurfaces
```
reaper.TrackList_UpdateAllExternalSurfaces()
```

No description available.
## Undo_BeginBlock
```
reaper.Undo_BeginBlock()
```

call to start a new block
## Undo_BeginBlock2
```
reaper.Undo_BeginBlock2(ReaProject proj)
```

call to start a new block
## Undo_CanRedo2
```
string reaper.Undo_CanRedo2(ReaProject proj)
```

returns string of next action,if able,NULL if not
## Undo_CanUndo2
```
string reaper.Undo_CanUndo2(ReaProject proj)
```

returns string of last action,if able,NULL if not
## Undo_DoRedo2
```
integer reaper.Undo_DoRedo2(ReaProject proj)
```

nonzero if success
## Undo_DoUndo2
```
integer reaper.Undo_DoUndo2(ReaProject proj)
```

nonzero if success
## Undo_EndBlock
```
reaper.Undo_EndBlock(string descchange, integer extraflags)
```

call to end the block,with extra flags if any,and a description
## Undo_EndBlock2
```
reaper.Undo_EndBlock2(ReaProject proj, string descchange, integer extraflags)
```

call to end the block,with extra flags if any,and a description
## Undo_OnStateChange
```
reaper.Undo_OnStateChange(string descchange)
```

limited state change to items
## Undo_OnStateChange2
```
reaper.Undo_OnStateChange2(ReaProject proj, string descchange)
```

limited state change to items
## Undo_OnStateChange_Item
```
reaper.Undo_OnStateChange_Item(ReaProject proj, string name, MediaItem item)
```

No description available.
## Undo_OnStateChangeEx
```
reaper.Undo_OnStateChangeEx(string descchange, integer whichStates, integer trackparm)
```

trackparm=-1 by default,or if updating one fx chain,you can specify track index
## Undo_OnStateChangeEx2
```
reaper.Undo_OnStateChangeEx2(ReaProject proj, string descchange, integer whichStates, integer trackparm)
```

trackparm=-1 by default,or if updating one fx chain,you can specify track index
## UpdateArrange
```
reaper.UpdateArrange()
```

Redraw the arrange view
## UpdateItemInProject
```
reaper.UpdateItemInProject(MediaItem item)
```

No description available.
## UpdateItemLanes
```
boolean reaper.UpdateItemLanes(ReaProject proj)
```

Recalculate lane arrangement for fixed lane tracks, including auto-removing empty lanes at the bottom of the track
## UpdateTimeline
```
reaper.UpdateTimeline()
```

Redraw the arrange view and ruler
## ValidatePtr
```
boolean reaper.ValidatePtr(identifier pointer, string ctypename)
```

see ValidatePtr2
## ValidatePtr2
```
boolean reaper.ValidatePtr2(ReaProject proj, identifier pointer, string ctypename)
```

Return true if the pointer is a valid object of the right type in proj (proj is ignored if pointer is itself a project). Supported types are: ReaProject*, MediaTrack*, MediaItem*, MediaItem_Take*, TrackEnvelope* and PCM_source*.
## ViewPrefs
```
reaper.ViewPrefs(integer page, string pageByName)
```

Opens the prefs to a page, use pageByName if page is 0.
## BR_EnvAlloc
```
BR_Envelope reaper.BR_EnvAlloc(TrackEnvelope envelope, boolean takeEnvelopesUseProjectTime)
```

[BR] Allocate envelope object from track or take envelope pointer. Always call BR_EnvFree when done to release the object and commit changes if needed. takeEnvelopesUseProjectTime: take envelope points' positions are counted from take position, not project start time. If you want to work with project time instead, pass this as true.
## BR_EnvCountPoints
```
integer reaper.BR_EnvCountPoints(BR_Envelope envelope)
```

[BR] Count envelope points in the envelope object allocated with BR_EnvAlloc.
## BR_EnvDeletePoint
```
boolean reaper.BR_EnvDeletePoint(BR_Envelope envelope, integer id)
```

[BR] Delete envelope point by index (zero-based) in the envelope object allocated with BR_EnvAlloc. Returns true on success.
## BR_EnvFind
```
integer reaper.BR_EnvFind(BR_Envelope envelope, number position, number delta)
```

[BR] Find envelope point at time position in the envelope object allocated with BR_EnvAlloc. Pass delta > 0 to search surrounding range - in that case the closest point to position within delta will be searched for. Returns envelope point id (zero-based) on success or -1 on failure.
## BR_EnvFindNext
```
integer reaper.BR_EnvFindNext(BR_Envelope envelope, number position)
```

[BR] Find next envelope point after time position in the envelope object allocated with BR_EnvAlloc. Returns envelope point id (zero-based) on success or -1 on failure.
## BR_EnvFindPrevious
```
integer reaper.BR_EnvFindPrevious(BR_Envelope envelope, number position)
```

[BR] Find previous envelope point before time position in the envelope object allocated with BR_EnvAlloc. Returns envelope point id (zero-based) on success or -1 on failure.
## BR_EnvFree
```
boolean reaper.BR_EnvFree(BR_Envelope envelope, boolean commit)
```

[BR] Free envelope object allocated with BR_EnvAlloc and commit changes if needed. Returns true if changes were committed successfully. Note that when envelope object wasn't modified nothing will get committed even if commit = true - in that case function returns false.
## BR_EnvGetParentTake
```
MediaItem_Take reaper.BR_EnvGetParentTake(BR_Envelope envelope)
```

[BR] If envelope object allocated with BR_EnvAlloc is take envelope, returns parent media item take, otherwise NULL.
## BR_EnvGetParentTrack
```
MediaTrack reaper.BR_EnvGetParentTrack(BR_Envelope envelope)
```

[BR] Get parent track of envelope object allocated with BR_EnvAlloc. If take envelope, returns NULL.
## BR_EnvGetPoint
```
boolean retval, number position, number value, integer shape, boolean selected, number bezier = reaper.BR_EnvGetPoint(BR_Envelope envelope, integer id)
```

[BR] Get envelope point by id (zero-based) from the envelope object allocated with BR_EnvAlloc. Returns true on success.
## BR_EnvGetProperties
```
boolean active, boolean visible, boolean armed, boolean inLane, integer laneHeight, integer defaultShape, number minValue, number maxValue, number centerValue, integer type, boolean faderScaling, optional integer automationItemsOptions = reaper.BR_EnvGetProperties(BR_Envelope envelope)
```

[BR] Get envelope properties for the envelope object allocated with BR_EnvAlloc.
## BR_EnvSetPoint
```
boolean reaper.BR_EnvSetPoint(BR_Envelope envelope, integer id, number position, number value, integer shape, boolean selected, number bezier)
```

[BR] Set envelope point by id (zero-based) in the envelope object allocated with BR_EnvAlloc. To create point instead, pass id = -1. Note that if new point is inserted or existing point's time position is changed, points won't automatically get sorted. To do that, see BR_EnvSortPoints.
Returns true on success.
## BR_EnvSetProperties
```
reaper.BR_EnvSetProperties(BR_Envelope envelope, boolean active, boolean visible, boolean armed, boolean inLane, integer laneHeight, integer defaultShape, boolean faderScaling, optional integer automationItemsOptionsIn)
```

[BR] Set envelope properties for the envelope object allocated with BR_EnvAlloc. For parameter description see BR_EnvGetProperties.
Setting automationItemsOptions requires REAPER 5.979+.
## BR_EnvSortPoints
```
reaper.BR_EnvSortPoints(BR_Envelope envelope)
```

[BR] Sort envelope points by position. The only reason to call this is if sorted points are explicitly needed after editing them with BR_EnvSetPoint. Note that you do not have to call this before doing BR_EnvFree since it does handle unsorted points too.
## BR_EnvValueAtPos
```
number reaper.BR_EnvValueAtPos(BR_Envelope envelope, number position)
```

[BR] Get envelope value at time position for the envelope object allocated with BR_EnvAlloc.
## BR_GetArrangeView
```
number startTime, number endTime = reaper.BR_GetArrangeView(ReaProject proj)
```

[BR] Deprecated, see GetSet_ArrangeView2 (REAPER v5.12pre4+) -- Get start and end time position of arrange view. To set arrange view instead, see BR_SetArrangeView.
## BR_GetClosestGridDivision
```
number reaper.BR_GetClosestGridDivision(number position)
```

[BR] Get closest grid division to position. Note that this functions is different from SnapToGrid in two regards. SnapToGrid() needs snap enabled to work and this one works always. Secondly, grid divisions are different from grid lines because some grid lines may be hidden due to zoom level - this function ignores grid line visibility and always searches for the closest grid division at given position. For more grid division functions, see BR_GetNextGridDivision and BR_GetPrevGridDivision.
## BR_GetCurrentTheme
```
string themePath, string themeName = reaper.BR_GetCurrentTheme()
```

[BR] Get current theme information. themePathOut is set to full theme path and themeNameOut is set to theme name excluding any path info and extension
## BR_GetMediaItemByGUID
```
MediaItem reaper.BR_GetMediaItemByGUID(ReaProject proj, string guidStringIn)
```

[BR] Get media item from GUID string. Note that the GUID must be enclosed in braces {}. To get item's GUID as a string, see BR_GetMediaItemGUID.
## BR_GetMediaItemGUID
```
string guidString = reaper.BR_GetMediaItemGUID(MediaItem item)
```

[BR] Get media item GUID as a string (guidStringOut_sz should be at least 64). To get media item back from GUID string, see BR_GetMediaItemByGUID.
## BR_GetMediaItemImageResource
```
boolean retval, string image, integer imageFlags = reaper.BR_GetMediaItemImageResource(MediaItem item)
```

[BR] Get currently loaded image resource and its flags for a given item. Returns false if there is no image resource set. To set image resource, see BR_SetMediaItemImageResource.
## BR_GetMediaItemTakeGUID
```
string guidString = reaper.BR_GetMediaItemTakeGUID(MediaItem_Take take)
```

[BR] Get media item take GUID as a string (guidStringOut_sz should be at least 64). To get take from GUID string, see SNM_GetMediaItemTakeByGUID.
## BR_GetMediaSourceProperties
```
boolean retval, boolean section, number start, number length, number fade, boolean reverse = reaper.BR_GetMediaSourceProperties(MediaItem_Take take)
```

[BR] Get take media source properties as they appear in Item properties. Returns false if take can't have them (MIDI items etc.).
To set source properties, see BR_SetMediaSourceProperties.
## BR_GetMediaTrackByGUID
```
MediaTrack reaper.BR_GetMediaTrackByGUID(ReaProject proj, string guidStringIn)
```

[BR] Get media track from GUID string. Note that the GUID must be enclosed in braces {}. To get track's GUID as a string, see GetSetMediaTrackInfo_String.
## BR_GetMediaTrackFreezeCount
```
integer reaper.BR_GetMediaTrackFreezeCount(MediaTrack track)
```

[BR] Get media track freeze count (if track isn't frozen at all, returns 0).
## BR_GetMediaTrackGUID
```
string guidString = reaper.BR_GetMediaTrackGUID(MediaTrack track)
```

[BR] Deprecated, see GetSetMediaTrackInfo_String (v5.95+). Get media track GUID as a string (guidStringOut_sz should be at least 64). To get media track back from GUID string, see BR_GetMediaTrackByGUID.
## BR_GetMediaTrackLayouts
```
string mcpLayoutName, string tcpLayoutName = reaper.BR_GetMediaTrackLayouts(MediaTrack track)
```

[BR] Deprecated, see GetSetMediaTrackInfo (REAPER v5.02+). Get media track layouts for MCP and TCP. Empty string ("") means that layout is set to the default layout. To set media track layouts, see BR_SetMediaTrackLayouts.
## BR_GetMediaTrackSendInfo_Envelope
```
TrackEnvelope reaper.BR_GetMediaTrackSendInfo_Envelope(MediaTrack track, integer category, integer sendidx, integer envelopeType)
```

[BR] Get track envelope for send/receive/hardware output.
## BR_GetMediaTrackSendInfo_Track
```
MediaTrack reaper.BR_GetMediaTrackSendInfo_Track(MediaTrack track, integer category, integer sendidx, integer trackType)
```

[BR] Get source or destination media track for send/receive.
## BR_GetMidiSourceLenPPQ
```
number reaper.BR_GetMidiSourceLenPPQ(MediaItem_Take take)
```

[BR] Get MIDI take source length in PPQ. In case the take isn't MIDI, return value will be -1.
## BR_GetMidiTakePoolGUID
```
boolean retval, string guidString = reaper.BR_GetMidiTakePoolGUID(MediaItem_Take take)
```

[BR] Get MIDI take pool GUID as a string (guidStringOut_sz should be at least 64). Returns true if take is pooled.
## BR_GetMidiTakeTempoInfo
```
boolean retval, boolean ignoreProjTempo, number bpm, integer num, integer den = reaper.BR_GetMidiTakeTempoInfo(MediaItem_Take take)
```

[BR] Get "ignore project tempo" information for MIDI take. Returns true if take can ignore project tempo (no matter if it's actually ignored), otherwise false.
## BR_GetMouseCursorContext
```
string window, string segment, string details = reaper.BR_GetMouseCursorContext()
```

[BR] Get mouse cursor context. Each parameter returns information in a form of string as specified in the table below.
## BR_GetMouseCursorContext_Envelope
```
TrackEnvelope retval, boolean takeEnvelope = reaper.BR_GetMouseCursorContext_Envelope()
```

[BR] Returns envelope that was captured with the last call to BR_GetMouseCursorContext. In case the envelope belongs to take, takeEnvelope will be true.
## BR_GetMouseCursorContext_Item
```
MediaItem reaper.BR_GetMouseCursorContext_Item()
```

[BR] Returns item under mouse cursor that was captured with the last call to BR_GetMouseCursorContext. Note that the function will return item even if mouse cursor is over some other track lane element like stretch marker or envelope. This enables for easier identification of items when you want to ignore elements within the item.
## BR_GetMouseCursorContext_MIDI
```
identifier retval, boolean inlineEditor, integer noteRow, integer ccLane, integer ccLaneVal, integer ccLaneId = reaper.BR_GetMouseCursorContext_MIDI()
```

[BR] Returns midi editor under mouse cursor that was captured with the last call to BR_GetMouseCursorContext.
## BR_GetMouseCursorContext_Position
```
number reaper.BR_GetMouseCursorContext_Position()
```

[BR] Returns project time position in arrange/ruler/midi editor that was captured with the last call to BR_GetMouseCursorContext.
## BR_GetMouseCursorContext_StretchMarker
```
integer reaper.BR_GetMouseCursorContext_StretchMarker()
```

[BR] Returns id of a stretch marker under mouse cursor that was captured with the last call to BR_GetMouseCursorContext.
## BR_GetMouseCursorContext_Take
```
MediaItem_Take reaper.BR_GetMouseCursorContext_Take()
```

[BR] Returns take under mouse cursor that was captured with the last call to BR_GetMouseCursorContext.
## BR_GetMouseCursorContext_Track
```
MediaTrack reaper.BR_GetMouseCursorContext_Track()
```

[BR] Returns track under mouse cursor that was captured with the last call to BR_GetMouseCursorContext.
## BR_GetNextGridDivision
```
number reaper.BR_GetNextGridDivision(number position)
```

[BR] Get next grid division after the time position. For more grid divisions function, see BR_GetClosestGridDivision and BR_GetPrevGridDivision.
## BR_GetPrevGridDivision
```
number reaper.BR_GetPrevGridDivision(number position)
```

[BR] Get previous grid division before the time position. For more grid division functions, see BR_GetClosestGridDivision and BR_GetNextGridDivision.
## BR_GetSetTrackSendInfo
```
number reaper.BR_GetSetTrackSendInfo(MediaTrack track, integer category, integer sendidx, string parmname, boolean setNewValue, number newValue)
```

[BR] Get or set send attributes.
## BR_GetTakeFXCount
```
integer reaper.BR_GetTakeFXCount(MediaItem_Take take)
```

[BR] Returns FX count for supplied take
## BR_IsMidiOpenInInlineEditor
```
boolean reaper.BR_IsMidiOpenInInlineEditor(MediaItem_Take take)
```

[SWS] Check if take has MIDI inline editor open and returns true or false.
## BR_IsTakeMidi
```
boolean retval, boolean inProjectMidi = reaper.BR_IsTakeMidi(MediaItem_Take take)
```

[BR] Check if take is MIDI take, in case MIDI take is in-project MIDI source data, inProjectMidiOut will be true, otherwise false.
## BR_ItemAtMouseCursor
```
MediaItem retval, number position = reaper.BR_ItemAtMouseCursor()
```

[BR] Get media item under mouse cursor. Position is mouse cursor position in arrange.
## BR_MIDI_CCLaneRemove
```
boolean reaper.BR_MIDI_CCLaneRemove(identifier midiEditor, integer laneId)
```

[BR] Remove CC lane in midi editor. Top visible CC lane is laneId 0. Returns true on success
## BR_MIDI_CCLaneReplace
```
boolean reaper.BR_MIDI_CCLaneReplace(identifier midiEditor, integer laneId, integer newCC)
```

[BR] Replace CC lane in midi editor. Top visible CC lane is laneId 0. Returns true on success.
Valid CC lanes: CC0-127=CC, 0x100|(0-31)=14-bit CC, 0x200=velocity, 0x201=pitch, 0x202=program, 0x203=channel pressure, 0x204=bank/program select, 0x205=text, 0x206=sysex, 0x207
## BR_PositionAtMouseCursor
```
number reaper.BR_PositionAtMouseCursor(boolean checkRuler)
```

[BR] Get position at mouse cursor. To check ruler along with arrange, pass checkRuler=true. Returns -1 if cursor is not over arrange/ruler.
## BR_SetArrangeView
```
reaper.BR_SetArrangeView(ReaProject proj, number startTime, number endTime)
```

[BR] Deprecated, see GetSet_ArrangeView2 (REAPER v5.12pre4+) -- Set start and end time position of arrange view. To get arrange view instead, see BR_GetArrangeView.
## BR_SetItemEdges
```
boolean reaper.BR_SetItemEdges(MediaItem item, number startTime, number endTime)
```

[BR] Set item start and end edges' position - returns true in case of any changes
## BR_SetMediaItemImageResource
```
reaper.BR_SetMediaItemImageResource(MediaItem item, string imageIn, integer imageFlags)
```

[BR] Set image resource and its flags for a given item. To clear current image resource, pass imageIn as "".
imageFlags: &1=0: don't display image, &1: center / tile, &3: stretch, &5: full height (REAPER 5.974+).
Can also be used to display existing text in empty items unstretched (pass imageIn = "", imageFlags = 0) or stretched (pass imageIn = "". imageFlags = 3).
To get image resource, see BR_GetMediaItemImageResource.
## BR_SetMediaSourceProperties
```
boolean reaper.BR_SetMediaSourceProperties(MediaItem_Take take, boolean section, number start, number length, number fade, boolean reverse)
```

[BR] Set take media source properties. Returns false if take can't have them (MIDI items etc.). Section parameters have to be valid only when passing section=true.
To get source properties, see BR_GetMediaSourceProperties.
## BR_SetMediaTrackLayouts
```
boolean reaper.BR_SetMediaTrackLayouts(MediaTrack track, string mcpLayoutNameIn, string tcpLayoutNameIn)
```

[BR] Deprecated, see GetSetMediaTrackInfo (REAPER v5.02+). Set media track layouts for MCP and TCP. To set default layout, pass empty string ("") as layout name. In case layouts were successfully set, returns true (if layouts are already set to supplied layout names, it will return false since no changes were made).
To get media track layouts, see BR_GetMediaTrackLayouts.
## BR_SetMidiTakeTempoInfo
```
boolean reaper.BR_SetMidiTakeTempoInfo(MediaItem_Take take, boolean ignoreProjTempo, number bpm, integer num, integer den)
```

[BR] Set "ignore project tempo" information for MIDI take. Returns true in case the take was successfully updated.
## BR_SetTakeSourceFromFile
```
boolean reaper.BR_SetTakeSourceFromFile(MediaItem_Take take, string filenameIn, boolean inProjectData)
```

[BR] Set new take source from file. To import MIDI file as in-project source data pass inProjectData=true. Returns false if failed.
Any take source properties from the previous source will be lost - to preserve them, see BR_SetTakeSourceFromFile2.
Note: To set source from existing take, see SNM_GetSetSourceState2.
## BR_SetTakeSourceFromFile2
```
boolean reaper.BR_SetTakeSourceFromFile2(MediaItem_Take take, string filenameIn, boolean inProjectData, boolean keepSourceProperties)
```

[BR] Differs from BR_SetTakeSourceFromFile only that it can also preserve existing take media source properties.
## BR_TakeAtMouseCursor
```
MediaItem_Take retval, number position = reaper.BR_TakeAtMouseCursor()
```

[BR] Get take under mouse cursor. Position is mouse cursor position in arrange.
## BR_TrackAtMouseCursor
```
MediaTrack retval, integer context, number position = reaper.BR_TrackAtMouseCursor()
```

[BR] Get track under mouse cursor.
Context signifies where the track was found: 0 = TCP, 1 = MCP, 2 = Arrange.
Position will hold mouse cursor position in arrange if applicable.
## BR_TrackFX_GetFXModuleName
```
boolean retval, string name = reaper.BR_TrackFX_GetFXModuleName(MediaTrack track, integer fx)
```

[BR] Deprecated, see TrackFX_GetNamedConfigParm/'fx_ident' (v6.37+). Get the exact name (like effect.dll, effect.vst3, etc...) of an FX.
## BR_Win32_CB_FindString
```
integer reaper.BR_Win32_CB_FindString(identifier comboBoxHwnd, integer startId, string string)
```

[BR] Equivalent to win32 API ComboBox_FindString().
## BR_Win32_CB_FindStringExact
```
integer reaper.BR_Win32_CB_FindStringExact(identifier comboBoxHwnd, integer startId, string string)
```

[BR] Equivalent to win32 API ComboBox_FindStringExact().
## BR_Win32_ClientToScreen
```
integer x, integer y = reaper.BR_Win32_ClientToScreen(identifier hwnd, integer xIn, integer yIn)
```

[BR] Equivalent to win32 API ClientToScreen().
## BR_Win32_FindWindowEx
```
identifier reaper.BR_Win32_FindWindowEx(string hwndParent, string hwndChildAfter, string className, string windowName, boolean searchClass, boolean searchName)
```

[BR] Equivalent to win32 API FindWindowEx(). Since ReaScript doesn't allow passing NULL (None in Python, nil in Lua etc...) parameters, to search by supplied class or name set searchClass and searchName accordingly. HWND parameters should be passed as either "0" to signify NULL or as string obtained from BR_Win32_HwndToString.
## BR_Win32_GET_X_LPARAM
```
integer reaper.BR_Win32_GET_X_LPARAM(integer lParam)
```

[BR] Equivalent to win32 API GET_X_LPARAM().
## BR_Win32_GET_Y_LPARAM
```
integer reaper.BR_Win32_GET_Y_LPARAM(integer lParam)
```

[BR] Equivalent to win32 API GET_Y_LPARAM().
## BR_Win32_GetConstant
```
integer reaper.BR_Win32_GetConstant(string constantName)
```

[BR] Returns various constants needed for BR_Win32 functions.
Supported constants are:
CB_ERR, CB_GETCOUNT, CB_GETCURSEL, CB_SETCURSEL
EM_SETSEL
GW_CHILD, GW_HWNDFIRST, GW_HWNDLAST, GW_HWNDNEXT, GW_HWNDPREV, GW_OWNER
GWL_STYLE
SW_HIDE, SW_MAXIMIZE, SW_SHOW, SW_SHOWMINIMIZED, SW_SHOWNA, SW_SHOWNOACTIVATE, SW_SHOWNORMAL
SWP_FRAMECHANGED, SWP_FRAMECHANGED, SWP_NOMOVE, SWP_NOOWNERZORDER, SWP_NOSIZE, SWP_NOZORDER
VK_DOWN, VK_UP
WM_CLOSE, WM_KEYDOWN
WS_MAXIMIZE, WS_OVERLAPPEDWINDOW
## BR_Win32_GetCursorPos
```
boolean retval, integer x, integer y = reaper.BR_Win32_GetCursorPos()
```

[BR] Equivalent to win32 API GetCursorPos().
## BR_Win32_GetFocus
```
identifier reaper.BR_Win32_GetFocus()
```

[BR] Equivalent to win32 API GetFocus().
## BR_Win32_GetForegroundWindow
```
identifier reaper.BR_Win32_GetForegroundWindow()
```

[BR] Equivalent to win32 API GetForegroundWindow().
## BR_Win32_GetMainHwnd
```
identifier reaper.BR_Win32_GetMainHwnd()
```

[BR] Alternative to GetMainHwnd. REAPER seems to have problems with extensions using HWND type for exported functions so all BR_Win32 functions use void* instead of HWND type
## BR_Win32_GetMixerHwnd
```
identifier retval, boolean isDocked = reaper.BR_Win32_GetMixerHwnd()
```

[BR] Get mixer window HWND. isDockedOut will be set to true if mixer is docked
## BR_Win32_GetMonitorRectFromRect
```
integer left, integer top, integer right, integer bottom = reaper.BR_Win32_GetMonitorRectFromRect(boolean workingAreaOnly, integer leftIn, integer topIn, integer rightIn, integer bottomIn)
```

[BR] Get coordinates for screen which is nearest to supplied coordinates. Pass workingAreaOnly as true to get screen coordinates excluding taskbar (or menu bar on OSX).
## BR_Win32_GetParent
```
identifier reaper.BR_Win32_GetParent(identifier hwnd)
```

[BR] Equivalent to win32 API GetParent().
## BR_Win32_GetPrivateProfileString
```
integer retval, string string = reaper.BR_Win32_GetPrivateProfileString(string sectionName, string keyName, string defaultString, string filePath)
```

[BR] Equivalent to win32 API GetPrivateProfileString(). For example, you can use this to get values from REAPER.ini.
## BR_Win32_GetWindow
```
identifier reaper.BR_Win32_GetWindow(identifier hwnd, integer cmd)
```

[BR] Equivalent to win32 API GetWindow().
## BR_Win32_GetWindowLong
```
integer reaper.BR_Win32_GetWindowLong(identifier hwnd, integer index)
```

[BR] Equivalent to win32 API GetWindowLong().
## BR_Win32_GetWindowRect
```
boolean retval, integer left, integer top, integer right, integer bottom = reaper.BR_Win32_GetWindowRect(identifier hwnd)
```

[BR] Equivalent to win32 API GetWindowRect().
## BR_Win32_GetWindowText
```
integer retval, string text = reaper.BR_Win32_GetWindowText(identifier hwnd)
```

[BR] Equivalent to win32 API GetWindowText().
## BR_Win32_HIBYTE
```
integer reaper.BR_Win32_HIBYTE(integer value)
```

[BR] Equivalent to win32 API HIBYTE().
## BR_Win32_HIWORD
```
integer reaper.BR_Win32_HIWORD(integer value)
```

[BR] Equivalent to win32 API HIWORD().
## BR_Win32_HwndToString
```
string string = reaper.BR_Win32_HwndToString(identifier hwnd)
```

[BR] Convert HWND to string. To convert string back to HWND, see BR_Win32_StringToHwnd.
## BR_Win32_IsWindow
```
boolean reaper.BR_Win32_IsWindow(identifier hwnd)
```

[BR] Equivalent to win32 API IsWindow().
## BR_Win32_IsWindowVisible
```
boolean reaper.BR_Win32_IsWindowVisible(identifier hwnd)
```

[BR] Equivalent to win32 API IsWindowVisible().
## BR_Win32_LOBYTE
```
integer reaper.BR_Win32_LOBYTE(integer value)
```

[BR] Equivalent to win32 API LOBYTE().
## BR_Win32_LOWORD
```
integer reaper.BR_Win32_LOWORD(integer value)
```

[BR] Equivalent to win32 API LOWORD().
## BR_Win32_MAKELONG
```
integer reaper.BR_Win32_MAKELONG(integer low, integer high)
```

[BR] Equivalent to win32 API MAKELONG().
## BR_Win32_MAKELPARAM
```
integer reaper.BR_Win32_MAKELPARAM(integer low, integer high)
```

[BR] Equivalent to win32 API MAKELPARAM().
## BR_Win32_MAKELRESULT
```
integer reaper.BR_Win32_MAKELRESULT(integer low, integer high)
```

[BR] Equivalent to win32 API MAKELRESULT().
## BR_Win32_MAKEWORD
```
integer reaper.BR_Win32_MAKEWORD(integer low, integer high)
```

[BR] Equivalent to win32 API MAKEWORD().
## BR_Win32_MAKEWPARAM
```
integer reaper.BR_Win32_MAKEWPARAM(integer low, integer high)
```

[BR] Equivalent to win32 API MAKEWPARAM().
## BR_Win32_MIDIEditor_GetActive
```
identifier reaper.BR_Win32_MIDIEditor_GetActive()
```

[BR] Alternative to MIDIEditor_GetActive. REAPER seems to have problems with extensions using HWND type for exported functions so all BR_Win32 functions use void* instead of HWND type.
## BR_Win32_ScreenToClient
```
integer x, integer y = reaper.BR_Win32_ScreenToClient(identifier hwnd, integer xIn, integer yIn)
```

[BR] Equivalent to win32 API ClientToScreen().
## BR_Win32_SendMessage
```
integer reaper.BR_Win32_SendMessage(identifier hwnd, integer msg, integer wParam, integer lParam)
```

[BR] Equivalent to win32 API SendMessage().
## BR_Win32_SetFocus
```
identifier reaper.BR_Win32_SetFocus(identifier hwnd)
```

[BR] Equivalent to win32 API SetFocus().
## BR_Win32_SetForegroundWindow
```
integer reaper.BR_Win32_SetForegroundWindow(identifier hwnd)
```

[BR] Equivalent to win32 API SetForegroundWindow().
## BR_Win32_SetWindowLong
```
integer reaper.BR_Win32_SetWindowLong(identifier hwnd, integer index, integer newLong)
```

[BR] Equivalent to win32 API SetWindowLong().
## BR_Win32_SetWindowPos
```
boolean reaper.BR_Win32_SetWindowPos(identifier hwnd, string hwndInsertAfter, integer x, integer y, integer width, integer height, integer flags)
```

[BR] Equivalent to win32 API SetWindowPos().
hwndInsertAfter may be a string: "HWND_BOTTOM", "HWND_NOTOPMOST", "HWND_TOP", "HWND_TOPMOST" or a string obtained with BR_Win32_HwndToString.
## BR_Win32_ShellExecute
```
integer reaper.BR_Win32_ShellExecute(string operation, string file, string parameters, string directory, integer showFlags)
```

[BR] Equivalent to win32 API ShellExecute() with HWND set to main window
## BR_Win32_ShowWindow
```
boolean reaper.BR_Win32_ShowWindow(identifier hwnd, integer cmdShow)
```

[BR] Equivalent to win32 API ShowWindow().
## BR_Win32_StringToHwnd
```
identifier reaper.BR_Win32_StringToHwnd(string string)
```

[BR] Convert string to HWND. To convert HWND back to string, see BR_Win32_HwndToString.
## BR_Win32_WindowFromPoint
```
identifier reaper.BR_Win32_WindowFromPoint(integer x, integer y)
```

[BR] Equivalent to win32 API WindowFromPoint().
## BR_Win32_WritePrivateProfileString
```
boolean reaper.BR_Win32_WritePrivateProfileString(string sectionName, string keyName, string value, string filePath)
```

[BR] Equivalent to win32 API WritePrivateProfileString(). For example, you can use this to write to REAPER.ini. You can pass an empty string as value to delete a key.
## Blink_GetAudioBufferTimingInfo
```
integer len, number srate, number time = reaper.Blink_GetAudioBufferTimingInfo()
```

Get audio buffer timing information. This is the length (size) of audio buffer in samples, sample rate and 'latest audio buffer switch wall clock time' in seconds.
## Blink_GetBeatAtTime
```
number reaper.Blink_GetBeatAtTime(number time, number quantum)
```

Get session beat value corresponding to given time for given quantum.
## Blink_GetClockNow
```
number reaper.Blink_GetClockNow()
```

Clock used by Blink.
## Blink_GetEnabled
```
boolean reaper.Blink_GetEnabled()
```

Is Blink currently enabled?
## Blink_GetMaster
```
boolean reaper.Blink_GetMaster()
```

Is Blink Master?
## Blink_GetNumPeers
```
integer reaper.Blink_GetNumPeers()
```

How many peers are currently connected in Link session?
## Blink_GetPhaseAtTime
```
number reaper.Blink_GetPhaseAtTime(number time, number quantum)
```

Get session phase at given time for given quantum.
## Blink_GetPlaying
```
boolean reaper.Blink_GetPlaying()
```

Is transport playing?
## Blink_GetPuppet
```
boolean reaper.Blink_GetPuppet()
```

Is Blink Puppet?
## Blink_GetQuantum
```
number reaper.Blink_GetQuantum()
```

Get quantum.
## Blink_GetStartStopSyncEnabled
```
boolean reaper.Blink_GetStartStopSyncEnabled()
```

Is start/stop synchronization enabled?
## Blink_GetTempo
```
number reaper.Blink_GetTempo()
```

Tempo of timeline, in quarter note Beats Per Minute.
## Blink_GetTimeAtBeat
```
number reaper.Blink_GetTimeAtBeat(number beat, number quantum)
```

Get time at which given beat occurs for given quantum.
## Blink_GetTimeForPlaying
```
number reaper.Blink_GetTimeForPlaying()
```

Get time at which transport start/stop occurs.
## Blink_GetTimelineOffset
```
number reaper.Blink_GetTimelineOffset()
```

Get timeline offset. This is the offset between REAPER timeline and Link session timeline.
## Blink_GetVersion
```
number reaper.Blink_GetVersion()
```

Get Blink version.
## Blink_SetBeatAtStartPlayingTimeRequest
```
reaper.Blink_SetBeatAtStartPlayingTimeRequest(number beat, number quantum)
```

Convenience function to attempt to map given beat to time when transport is starting to play in context of given quantum. This function evaluates to a no-op if GetPlaying() equals false.
## Blink_SetBeatAtTimeForce
```
reaper.Blink_SetBeatAtTimeForce(number bpm, number time, number quantum)
```

Rudely re-map beat/time relationship for all peers in Link session.
## Blink_SetBeatAtTimeRequest
```
reaper.Blink_SetBeatAtTimeRequest(number bpm, number time, number quantum)
```

Attempt to map given beat to given time in context of given quantum.
## Blink_SetCaptureTransportCommands
```
reaper.Blink_SetCaptureTransportCommands(boolean enable)
```

Captures REAPER Transport commands and 'Tempo: Increase/Decrease current project tempo by' commands and broadcasts them into Link session. When used with Master or Puppet mode enabled, provides better integration between REAPER and Link session transport and tempos.
## Blink_SetEnabled
```
reaper.Blink_SetEnabled(boolean enable)
```

Enable/disable Blink. In Blink methods transport, tempo and timeline refer to Link session, not local REAPER instance.
## Blink_SetLaunchOffset
```
reaper.Blink_SetLaunchOffset(number offset)
```

Set launch offset. This is used to compensate for possible constant REAPER transport launch delay, if such exists.
## Blink_SetMaster
```
reaper.Blink_SetMaster(boolean enable)
```

Set Blink as Master. Puppet needs to be enabled first. Same as Puppet, but possible beat offset is broadcast to Link session, effectively forcing local REAPER timeline on peers. Only one, if any, Blink should be Master in Link session.
## Blink_SetPlaying
```
reaper.Blink_SetPlaying(boolean playing, number time)
```

Set if transport should be playing or stopped, taking effect at given time.
## Blink_SetPlayingAndBeatAtTimeRequest
```
reaper.Blink_SetPlayingAndBeatAtTimeRequest(boolean playing, number time, number beat, number quantum)
```

Convenience function to start or stop transport at given time and attempt to map given beat to this time in context of given quantum.
## Blink_SetPuppet
```
reaper.Blink_SetPuppet(boolean enable)
```

Set Blink as Puppet. When enabled, Blink attempts to synchronize local REAPER tempo to Link session tempo by adjusting current active tempo/time signature marker, or broadcasts local REAPER tempo changes into Link session, and attempts to correct possible offset by adjusting REAPER playrate. Based on cumulative single beat phase since Link session transport start, regardless of quantum.
## Blink_SetQuantum
```
reaper.Blink_SetQuantum(number quantum)
```

Set quantum. Usually this is set to length of one measure/bar in quarter notes.
## Blink_SetStartStopSyncEnabled
```
reaper.Blink_SetStartStopSyncEnabled(boolean enable)
```

Enable start/stop synchronization.
## Blink_SetTempo
```
reaper.Blink_SetTempo(number bpm)
```

Set timeline tempo to given bpm value.
## Blink_SetTempoAtTime
```
reaper.Blink_SetTempoAtTime(number bpm, number time)
```

Set tempo to given bpm value, taking effect (heard from speakers)at given wall clock time.
## Blink_StartStop
```
reaper.Blink_StartStop()
```

Transport start/stop.
## CF_CreatePreview
```
CF_Preview reaper.CF_CreatePreview(PCM_source source)
```

Create a new preview object. Does not take ownership of the source (don't forget to destroy it unless it came from a take!). See CF_Preview_Play and the others CF_Preview_* functions.
## CF_EnumMediaSourceCues
```
integer retval, number time, number endTime, boolean isRegion, string name, boolean isChapter = reaper.CF_EnumMediaSourceCues(PCM_source src, integer index)
```

Enumerate the source's media cues. Returns the next index or 0 when finished.
## CF_EnumSelectedFX
```
integer reaper.CF_EnumSelectedFX(FxChain hwnd, integer index)
```

Return the index of the next selected effect in the given FX chain. Start index should be -1. Returns -1 if there are no more selected effects.
## CF_EnumerateActions
```
integer retval, string name = reaper.CF_EnumerateActions(integer section, integer index)
```

Deprecated, see kbd_enumerateActions (v6.71+). Wrapper for the unexposed kbd_enumerateActions API function.
Main=0, Main (alt recording)=100, MIDI Editor=32060, MIDI Event List Editor=32061, MIDI Inline Editor=32062, Media Explorer=32063
## CF_ExportMediaSource
```
boolean reaper.CF_ExportMediaSource(PCM_source src, string fn)
```

Export the source to the given file (MIDI only).
## CF_GetClipboard
```
string text = reaper.CF_GetClipboard()
```

Read the contents of the system clipboard.
## CF_GetClipboardBig
```
string reaper.CF_GetClipboardBig(WDL_FastString output)
```

[DEPRECATED: Use CF_GetClipboard] Read the contents of the system clipboard. See SNM_CreateFastString and SNM_DeleteFastString.
## CF_GetCommandText
```
string reaper.CF_GetCommandText(integer section, integer command)
```

Deprecated, see kbd_getTextFromCmd (v6.71+). Wrapper for the unexposed kbd_getTextFromCmd API function. See CF_EnumerateActions for common section IDs.
## CF_GetCustomColor
```
integer reaper.CF_GetCustomColor(integer index)
```

Get one of 16 SWS custom colors (0xBBGGRR on Windows, 0xRRGGBB everyhwere else). Index is zero-based.
## CF_GetFocusedFXChain
```
FxChain = reaper.CF_GetFocusedFXChain()
```

Return a handle to the currently focused FX chain window.
## CF_GetMediaSourceBitDepth
```
integer reaper.CF_GetMediaSourceBitDepth(PCM_source src)
```

Returns the bit depth if available (0 otherwise).
## CF_GetMediaSourceBitRate
```
number reaper.CF_GetMediaSourceBitRate(PCM_source src)
```

Returns the bit rate for WAVE (wav, aif) and streaming/variable formats (mp3, ogg, opus). REAPER v6.19 or later is required for non-WAVE formats.
## CF_GetMediaSourceMetadata
```
boolean retval, string out = reaper.CF_GetMediaSourceMetadata(PCM_source src, string name, string out)
```

Get the value of the given metadata field (eg. DESC, ORIG, ORIGREF, DATE, TIME, UMI, CODINGHISTORY for BWF).
## CF_GetMediaSourceOnline
```
boolean reaper.CF_GetMediaSourceOnline(PCM_source src)
```

Returns the online/offline status of the given source.
## CF_GetMediaSourceRPP
```
boolean retval, string fn = reaper.CF_GetMediaSourceRPP(PCM_source src)
```

Get the project associated with this source (BWF, subproject...).
## CF_GetSWSVersion
```
string version = reaper.CF_GetSWSVersion()
```

Return the current SWS version number.
## CF_GetTakeFXChain
```
FxChain reaper.CF_GetTakeFXChain(MediaItem_Take take)
```

Return a handle to the given take FX chain window. HACK: This temporarily renames the take in order to disambiguate the take FX chain window from similarily named takes.
## CF_GetTrackFXChain
```
FxChain reaper.CF_GetTrackFXChain(MediaTrack track)
```

Return a handle to the given track FX chain window.
## CF_GetTrackFXChainEx
```
FxChain reaper.CF_GetTrackFXChainEx(ReaProject project, MediaTrack track, boolean wantInputChain)
```

Return a handle to the given track FX chain window. Set wantInputChain to get the track's input/monitoring FX chain.
## CF_LocateInExplorer
```
boolean reaper.CF_LocateInExplorer(string file)
```

Select the given file in explorer/finder.
## CF_NormalizeUTF8
```
string normalized = reaper.CF_NormalizeUTF8(string input, integer mode)
```

Apply Unicode normalization to the provided UTF-8 string.
## CF_PCM_Source_SetSectionInfo
```
boolean reaper.CF_PCM_Source_SetSectionInfo(PCM_source section, PCM_source source, number offset, number length, boolean reverse, optional number fadeIn)
```

Give a section source created using PCM_Source_CreateFromType("SECTION"). Offset and length are ignored if 0. Negative length to subtract from the total length of the source.
## CF_Preview_GetOutputTrack
```
MediaTrack reaper.CF_Preview_GetOutputTrack(CF_Preview preview)
```

No description available.
## CF_Preview_GetPeak
```
boolean retval, number peakvol = reaper.CF_Preview_GetPeak(CF_Preview preview, integer channel)
```

Return the maximum sample value played since the last read. Refresh speed depends on buffer size.
## CF_Preview_GetValue
```
boolean retval, number value = reaper.CF_Preview_GetValue(CF_Preview preview, string name)
```

Supported attributes:
B_LOOP seek to the beginning when reaching the end of the source
B_PPITCH preserve pitch when changing playback rate
D_FADEINLEN length in seconds of playback fade in
D_FADEOUTLEN length in seconds of playback fade out
D_LENGTH (read only) length of the source * playback rate
D_MEASUREALIGN >0 = wait until the next bar before starting playback (note: this causes playback to silently continue when project is paused and previewing through a track)
D_PAN playback pan
D_PITCH pitch adjustment in semitones
D_PLAYRATE playback rate (0.01..100)
D_POSITION current playback position
D_VOLUME playback volume
I_OUTCHAN first hardware output channel (&1024=mono, reads -1 when playing through a track, see CF_Preview_SetOutputTrack)
I_PITCHMODE highest 16 bits=pitch shift mode (see EnumPitchShiftModes), lower 16 bits=pitch shift submode (see EnumPitchShiftSubModes)
## CF_Preview_Play
```
boolean reaper.CF_Preview_Play(CF_Preview preview)
```

Start playback of the configured preview object.
## CF_Preview_SetOutputTrack
```
boolean reaper.CF_Preview_SetOutputTrack(CF_Preview preview, ReaProject project, MediaTrack track)
```

No description available.
## CF_Preview_SetValue
```
boolean reaper.CF_Preview_SetValue(CF_Preview preview, string name, number newValue)
```

See CF_Preview_GetValue.
## CF_Preview_Stop
```
boolean reaper.CF_Preview_Stop(CF_Preview preview)
```

Stop and destroy a preview object.
## CF_Preview_StopAll
```
reaper.CF_Preview_StopAll()
```

Stop and destroy all currently active preview objects.
## CF_SelectTakeFX
```
boolean reaper.CF_SelectTakeFX(MediaItem_Take take, integer index)
```

Set which take effect is active in the take's FX chain. The FX chain window does not have to be open.
## CF_SelectTrackFX
```
boolean reaper.CF_SelectTrackFX(MediaTrack track, integer index)
```

Set which track effect is active in the track's FX chain. The FX chain window does not have to be open.
## CF_SendActionShortcut
```
boolean reaper.CF_SendActionShortcut(identifier hwnd, integer section, integer key, optional integer modifiersIn)
```

Run in the specified window the action command ID associated with the shortcut key in the given section. See CF_EnumerateActions for common section IDs.
## CF_SetClipboard
```
reaper.CF_SetClipboard(string str)
```

Write the given string into the system clipboard.
## CF_SetCustomColor
```
reaper.CF_SetCustomColor(integer index, integer color)
```

Set one of 16 SWS custom colors (0xBBGGRR on Windows, 0xRRGGBB everyhwere else). Index is zero-based.
## CF_SetMediaSourceOnline
```
reaper.CF_SetMediaSourceOnline(PCM_source src, boolean set)
```

Set the online/offline status of the given source (closes files when set=false).
## CF_ShellExecute
```
boolean reaper.CF_ShellExecute(string file)
```

Open the given file or URL in the default application. See also CF_LocateInExplorer.
## CreateChildWindowForHWND
```
identifier reaper.CreateChildWindowForHWND(identifier parentHWND, string title)
```

(MIDI Razor Edits only for the time being) Create a new Win32 HWND floating above an existing HWND.
## DestroyChildWindow
```
boolean reaper.DestroyChildWindow(identifier childHWND)
```

(MIDI Razor Edits only for the time being) Destroy an HWND created by CreateChildWindowForHWND.
## FNG_AddMidiNote
```
RprMidiNote reaper.FNG_AddMidiNote(RprMidiTake midiTake)
```

[FNG] Add MIDI note to MIDI take
## FNG_AllocMidiTake
```
RprMidiTake reaper.FNG_AllocMidiTake(MediaItem_Take take)
```

[FNG] Allocate a RprMidiTake from a take pointer. Returns a NULL pointer if the take is not an in-project MIDI take
## FNG_CountMidiNotes
```
integer reaper.FNG_CountMidiNotes(RprMidiTake midiTake)
```

[FNG] Count of how many MIDI notes are in the MIDI take
## FNG_FreeMidiTake
```
reaper.FNG_FreeMidiTake(RprMidiTake midiTake)
```

[FNG] Commit changes to MIDI take and free allocated memory
## FNG_GetMidiNote
```
RprMidiNote reaper.FNG_GetMidiNote(RprMidiTake midiTake, integer index)
```

[FNG] Get a MIDI note from a MIDI take at specified index
## FNG_GetMidiNoteIntProperty
```
integer reaper.FNG_GetMidiNoteIntProperty(RprMidiNote midiNote, string property)
```

[FNG] Get MIDI note property. Supported properties: CHANNEL, LENGTH, MUTED, PITCH, POSITION, SELECTED and VELOCITY.
## FNG_SetMidiNoteIntProperty
```
reaper.FNG_SetMidiNoteIntProperty(RprMidiNote midiNote, string property, integer value)
```

[FNG] Set MIDI note property. See FNG_GetMidiNoteIntProperty for the list of supported properties.
## Fab_Clear
```
boolean reaper.Fab_Clear(optional string idStringIn)
```

Clears ReaFab control map, optionally based on matching idString. Returns true on success.
## Fab_Do
```
boolean reaper.Fab_Do(integer command, integer val)
```

Runs ReaFab actions/commands. First parameter (command) is ReaFab command number, e.g. 3 for 3rd encoder rotation. Second parameter (val) is MIDI CC Relative value. Value 1 is increment of 1, 127 is decrement of 1. 2 is inc 2, 126 is dec 2 and so on. For button press (commands 9-32) a value of 127 is recommended.
## Fab_Dump
```
reaper.Fab_Dump()
```

Dumps current control mapping into .lua file under ResourcePath/Scripts/reafab_dump-timestamp.lua
## Fab_Get
```
boolean retval, integer fx, integer param = reaper.Fab_Get(integer command)
```

Returns target FX and parameter index for given ReaFab command in context of selected track and ReaFab FX index. Valid command range 1 ... 24. Returns false if no such command mapping is found. Returns param index -1 for ReaFab internal band change command.
## Fab_Map
```
boolean reaper.Fab_Map(string fxId, integer command, string paramId, integer control, optional integer bandsIn, optional number stepIn, optional number accelIn, optional number minvalIn, optional number maxvalIn)
```

Creates control mapping for ReaFab command.
fxId e.g. "ReaComp".
command 1-8 for encoders, 9-24 for buttons.
paramId e.g. "Ratio".
control 1 = direct, 2 = band selector, 3 = cycle, 4 = invert, 5 = force toggle, 6 = force range, 7 = 5 and 6, 8 = force continuous.
bands define, if target fx has multiple identical target bands. In this case, paramId must include 00 placeholder, e.g. "Band 00 Gain".
step overrides built-in default step of ~0.001 for continuous parameters.
accel overrides built-in default control acceleration step of 1.0.
minval & maxval override default detected target param value range.
Prefixing paramId with "-" reverses direction; useful for creating separate next/previous mappings for bands or list type value navigation.
## GU_Config_Read
```
boolean retval, string value = reaper.GU_Config_Read(string fileName, string category, string key)
```

Reads from a config file in the GUtilities folder in Reaper's resource folder
## GU_Config_Write
```
boolean reaper.GU_Config_Write(string fileName, string category, string key, string value)
```

Writes a config file to the GUtilities folder in Reaper's resource folder
## GU_Filesystem_CountMediaFiles
```
integer retval, number fileSize = reaper.GU_Filesystem_CountMediaFiles(string path, integer flags)
```

Returns count and filesize in megabytes for all valid media files within the path. Returns -1 if path is invalid. Flags can be passed as an argument to determine which media files are valid. A flag with a value of -1 will reset the cache, otherwise, the following flags can be used: ALL = 0, WAV = 1, AIFF = 2, FLAC = 4, MP3 = 8, OGG = 16, BWF = 32, W64 = 64, WAVPACK = 128, GIF = 256, MP4 = 512
## GU_Filesystem_EnumerateMediaFiles
```
string path = reaper.GU_Filesystem_EnumerateMediaFiles(string path, integer flags)
```

Returns the next valid file in a directory each time this function is called with the same path. Returns an empty string if path does not contain any more valid files. Flags can be passed as an argument to determine which media files are valid. A flag with a value of -1 will reset the cache, otherwise, the following flags can be used: ALL = 0, WAV = 1, AIFF = 2, FLAC = 4, MP3 = 8, OGG = 16, BWF = 32, W64 = 64, WAVPACK = 128, GIF = 256, MP4 = 512
## GU_Filesystem_FindFileInPath
```
string path = reaper.GU_Filesystem_FindFileInPath(string path, string fileName)
```

Returns the first found file's path from within a given path. Returns an empty string if not found
## GU_Filesystem_PathExists
```
boolean reaper.GU_Filesystem_PathExists(string path)
```

Checks if file or directory exists
## GU_GUtilitiesAPI_GetVersion
```
string version = reaper.GU_GUtilitiesAPI_GetVersion()
```

Gets the current GUtilitiesAPI version
## GU_PCM_Source_GetSampleValue
```
number reaper.GU_PCM_Source_GetSampleValue(PCM_source source, number time)
```

Gets a PCM_source's sample value at a point in time (seconds)
## GU_PCM_Source_HasRegion
```
boolean reaper.GU_PCM_Source_HasRegion(PCM_source source)
```

Checks if PCM_source has embedded Media Cue Markers
## GU_PCM_Source_IsMono
```
boolean reaper.GU_PCM_Source_IsMono(PCM_source source)
```

Checks if PCM_source is mono by comparing all channels
## GU_PCM_Source_TimeToPeak
```
number reaper.GU_PCM_Source_TimeToPeak(PCM_source source, integer bufferSize, number threshold)
```

Returns duration in seconds for PCM_source from start til peak threshold is breached. Returns -1 if invalid
## GU_PCM_Source_TimeToPeakR
```
number reaper.GU_PCM_Source_TimeToPeakR(PCM_source source, integer bufferSize, number threshold)
```

Returns duration in seconds for PCM_source from end til peak threshold is breached in reverse. Returns -1 if invalid
## GU_PCM_Source_TimeToRMS
```
number reaper.GU_PCM_Source_TimeToRMS(PCM_source source, integer bufferSize, number threshold)
```

Returns duration in seconds for PCM_source from start til RMS threshold is breached. Returns -1 if invalid
## GU_PCM_Source_TimeToRMSR
```
number reaper.GU_PCM_Source_TimeToRMSR(PCM_source source, integer bufferSize, number threshold)
```

Returns duration in seconds for PCM_source from end til RMS threshold is breached in reverse. Returns -1 if invalid
## GU_WildcardParseTake
```
string value = reaper.GU_WildcardParseTake(MediaItem_Take take, string input)
```

Returns a string by parsing wildcards relative to the supplied MediaItem_Take
## ImGui_AcceptDragDropPayload
```
boolean retval, string payload = reaper.ImGui_AcceptDragDropPayload(ImGui_Context ctx, string type, string payload, optional integer flagsIn)
```

Accept contents of a given type. If DragDropFlags_AcceptBeforeDelivery is set
you can peek into the payload before the mouse button is released.
## ImGui_AcceptDragDropPayloadFiles
```
boolean retval, integer count = reaper.ImGui_AcceptDragDropPayloadFiles(ImGui_Context ctx, integer count, optional integer flagsIn)
```

Accept a list of dropped files. See AcceptDragDropPayload and GetDragDropPayloadFile.
## ImGui_AcceptDragDropPayloadRGB
```
boolean retval, integer rgb = reaper.ImGui_AcceptDragDropPayloadRGB(ImGui_Context ctx, integer rgb, optional integer flagsIn)
```

Accept a RGB color. See AcceptDragDropPayload.
## ImGui_AcceptDragDropPayloadRGBA
```
boolean retval, integer rgba = reaper.ImGui_AcceptDragDropPayloadRGBA(ImGui_Context ctx, integer rgba, optional integer flagsIn)
```

Accept a RGBA color. See AcceptDragDropPayload.
## ImGui_AlignTextToFramePadding
```
reaper.ImGui_AlignTextToFramePadding(ImGui_Context ctx)
```

Vertically align upcoming text baseline to StyleVar_FramePadding.y so that it
will align properly to regularly framed items (call if you have text on a line
before a framed item).
## ImGui_ArrowButton
```
boolean reaper.ImGui_ArrowButton(ImGui_Context ctx, string str_id, integer dir)
```

Square button with an arrow shape. 'dir' is one of the Dir_* values
## ImGui_Attach
```
reaper.ImGui_Attach(ImGui_Context ctx, ImGui_Resource obj)
```

Link the object's lifetime to the given context.
Objects can be draw list splitters, fonts, images, list clippers, etc.
Call Detach to let the object be garbage-collected after unuse again.
## ImGui_Begin
```
boolean retval, optional boolean p_open = reaper.ImGui_Begin(ImGui_Context ctx, string name, optional boolean p_open, optional integer flagsIn)
```

Push window to the stack and start appending to it.
## ImGui_BeginChild
```
boolean reaper.ImGui_BeginChild(ImGui_Context ctx, string str_id, optional number size_wIn, optional number size_hIn, optional integer child_flagsIn, optional integer window_flagsIn)
```

Manual sizing (each axis can use a different setting e.g. size_w=0 and size_h=400):
- = 0.0: use remaining parent window size for this axis
- \> 0.0: use specified size for this axis
- < 0.0: right/bottom-align to specified distance from available content boundaries
## ImGui_BeginCombo
```
boolean reaper.ImGui_BeginCombo(ImGui_Context ctx, string label, string preview_value, optional integer flagsIn)
```

The BeginCombo/EndCombo API allows you to manage your contents and selection
state however you want it, by creating e.g. Selectable items.
## ImGui_BeginDisabled
```
reaper.ImGui_BeginDisabled(ImGui_Context ctx, optional boolean disabledIn)
```

Disable all user interactions and dim items visuals
(applying StyleVar_DisabledAlpha over current colors).
## ImGui_BeginDragDropSource
```
boolean reaper.ImGui_BeginDragDropSource(ImGui_Context ctx, optional integer flagsIn)
```

Call after submitting an item which may be dragged. when this return true,
you can call SetDragDropPayload() + EndDragDropSource()
## ImGui_BeginDragDropTarget
```
boolean reaper.ImGui_BeginDragDropTarget(ImGui_Context ctx)
```

Call after submitting an item that may receive a payload.
If this returns true, you can call AcceptDragDropPayload + EndDragDropTarget.
## ImGui_BeginGroup
```
reaper.ImGui_BeginGroup(ImGui_Context ctx)
```

Lock horizontal starting position. See EndGroup.
## ImGui_BeginItemTooltip
```
boolean reaper.ImGui_BeginItemTooltip(ImGui_Context ctx)
```

Begin/append a tooltip window if preceding item was hovered. Shortcut for
`IsItemHovered(HoveredFlags_ForTooltip) && BeginTooltip()`.
## ImGui_BeginListBox
```
boolean reaper.ImGui_BeginListBox(ImGui_Context ctx, string label, optional number size_wIn, optional number size_hIn)
```

Open a framed scrolling region.
## ImGui_BeginMenu
```
boolean reaper.ImGui_BeginMenu(ImGui_Context ctx, string label, optional boolean enabledIn)
```

Create a sub-menu entry. only call EndMenu if this returns true!
## ImGui_BeginMenuBar
```
boolean reaper.ImGui_BeginMenuBar(ImGui_Context ctx)
```

Append to menu-bar of current window (requires WindowFlags_MenuBar flag set
on parent window). See EndMenuBar.
## ImGui_BeginPopup
```
boolean reaper.ImGui_BeginPopup(ImGui_Context ctx, string str_id, optional integer flagsIn)
```

Query popup state, if open start appending into the window. Call EndPopup
afterwards if returned true. WindowFlags* are forwarded to the window.
## ImGui_BeginPopupContextItem
```
boolean reaper.ImGui_BeginPopupContextItem(ImGui_Context ctx, optional string str_idIn, optional integer popup_flagsIn)
```

This is a helper to handle the simplest case of associating one named popup
to one given widget. You can pass a nil str_id to use the identifier of the last
item. This is essentially the same as calling OpenPopupOnItemClick + BeginPopup
but written to avoid computing the ID twice because BeginPopupContext*
functions may be called very frequently.
## ImGui_BeginPopupContextWindow
```
boolean reaper.ImGui_BeginPopupContextWindow(ImGui_Context ctx, optional string str_idIn, optional integer popup_flagsIn)
```

Open+begin popup when clicked on current window.
## ImGui_BeginPopupModal
```
boolean retval, optional boolean p_open = reaper.ImGui_BeginPopupModal(ImGui_Context ctx, string name, optional boolean p_open, optional integer flagsIn)
```

Block every interaction behind the window, cannot be closed by user, add a
dimming background, has a title bar. Return true if the modal is open, and you
can start outputting to it. See BeginPopup.
## ImGui_BeginTabBar
```
boolean reaper.ImGui_BeginTabBar(ImGui_Context ctx, string str_id, optional integer flagsIn)
```

Create and append into a TabBar.
## ImGui_BeginTabItem
```
boolean retval, optional boolean p_open = reaper.ImGui_BeginTabItem(ImGui_Context ctx, string label, optional boolean p_open, optional integer flagsIn)
```

Create a Tab. Returns true if the Tab is selected.
Set 'p_open' to true to enable the close button.
## ImGui_BeginTable
```
boolean reaper.ImGui_BeginTable(ImGui_Context ctx, string str_id, integer columns, optional integer flagsIn, optional number outer_size_wIn, optional number outer_size_hIn, optional number inner_widthIn)
```

No description available.
## ImGui_BeginTooltip
```
boolean reaper.ImGui_BeginTooltip(ImGui_Context ctx)
```

Begin/append a tooltip window.
## ImGui_Bullet
```
reaper.ImGui_Bullet(ImGui_Context ctx)
```

Draw a small circle + keep the cursor on the same line.
Advance cursor x position by GetTreeNodeToLabelSpacing,
same distance that TreeNode uses.
## ImGui_BulletText
```
reaper.ImGui_BulletText(ImGui_Context ctx, string text)
```

Shortcut for Bullet + Text.
## ImGui_Button
```
boolean reaper.ImGui_Button(ImGui_Context ctx, string label, optional number size_wIn, optional number size_hIn)
```

No description available.
## ImGui_ButtonFlags_MouseButtonLeft
```
integer reaper.ImGui_ButtonFlags_MouseButtonLeft()
```

React on left mouse button (default).
## ImGui_ButtonFlags_MouseButtonMiddle
```
integer reaper.ImGui_ButtonFlags_MouseButtonMiddle()
```

React on center mouse button.
## ImGui_ButtonFlags_MouseButtonRight
```
integer reaper.ImGui_ButtonFlags_MouseButtonRight()
```

React on right mouse button.
## ImGui_ButtonFlags_None
```
integer reaper.ImGui_ButtonFlags_None()
```

No description available.
## ImGui_CalcItemWidth
```
number reaper.ImGui_CalcItemWidth(ImGui_Context ctx)
```

Width of item given pushed settings and current cursor position.
NOT necessarily the width of last item unlike most 'Item' functions.
## ImGui_CalcTextSize
```
number w, number h = reaper.ImGui_CalcTextSize(ImGui_Context ctx, string text, number w, number h, optional boolean hide_text_after_double_hashIn, optional number wrap_widthIn)
```

No description available.
## ImGui_Checkbox
```
boolean retval, boolean v = reaper.ImGui_Checkbox(ImGui_Context ctx, string label, boolean v)
```

No description available.
## ImGui_CheckboxFlags
```
boolean retval, integer flags = reaper.ImGui_CheckboxFlags(ImGui_Context ctx, string label, integer flags, integer flags_value)
```

No description available.
## ImGui_ChildFlags_AlwaysAutoResize
```
integer reaper.ImGui_ChildFlags_AlwaysAutoResize()
```

Combined with AutoResizeX/AutoResizeY. Always measure size even when child
is hidden, always return true, always disable clipping optimization! NOT RECOMMENDED.
## ImGui_ChildFlags_AlwaysUseWindowPadding
```
integer reaper.ImGui_ChildFlags_AlwaysUseWindowPadding()
```

Pad with StyleVar_WindowPadding even if no border are drawn (no padding by
default for non-bordered child windows because it makes more sense).
## ImGui_ChildFlags_AutoResizeX
```
integer reaper.ImGui_ChildFlags_AutoResizeX()
```

Enable auto-resizing width. Read notes above.
## ImGui_ChildFlags_AutoResizeY
```
integer reaper.ImGui_ChildFlags_AutoResizeY()
```

Enable auto-resizing height. Read notes above.
## ImGui_ChildFlags_Border
```
integer reaper.ImGui_ChildFlags_Border()
```

Show an outer border and enable WindowPadding.
## ImGui_ChildFlags_FrameStyle
```
integer reaper.ImGui_ChildFlags_FrameStyle()
```

Style the child window like a framed item: use Col_FrameBg, StyleVar_FrameRounding, StyleVar_FrameBorderSize, StyleVar_FramePadding instead of Col_ChildBg, StyleVar_ChildRounding, StyleVar_ChildBorderSize, StyleVar_WindowPadding.
## ImGui_ChildFlags_NavFlattened
```
integer reaper.ImGui_ChildFlags_NavFlattened()
```

Share focus scope, allow gamepad/keyboard navigation to cross over parent border to this child or between sibling child windows.
## ImGui_ChildFlags_None
```
integer reaper.ImGui_ChildFlags_None()
```

No description available.
## ImGui_ChildFlags_ResizeX
```
integer reaper.ImGui_ChildFlags_ResizeX()
```

Allow resize from right border (layout direction).
Enables .ini saving (unless WindowFlags_NoSavedSettings passed to window flags).
## ImGui_ChildFlags_ResizeY
```
integer reaper.ImGui_ChildFlags_ResizeY()
```

Allow resize from bottom border (layout direction).
Enables .ini saving (unless WindowFlags_NoSavedSettings passed to window flags).
## ImGui_CloseCurrentPopup
```
reaper.ImGui_CloseCurrentPopup(ImGui_Context ctx)
```

Manually close the popup we have begin-ed into.
Use inside the BeginPopup/EndPopup scope to close manually.
## ImGui_Col_Border
```
integer reaper.ImGui_Col_Border()
```

No description available.
## ImGui_Col_BorderShadow
```
integer reaper.ImGui_Col_BorderShadow()
```

No description available.
## ImGui_Col_Button
```
integer reaper.ImGui_Col_Button()
```

No description available.
## ImGui_Col_ButtonActive
```
integer reaper.ImGui_Col_ButtonActive()
```

No description available.
## ImGui_Col_ButtonHovered
```
integer reaper.ImGui_Col_ButtonHovered()
```

No description available.
## ImGui_Col_CheckMark
```
integer reaper.ImGui_Col_CheckMark()
```

Checkbox tick and RadioButton circle
## ImGui_Col_ChildBg
```
integer reaper.ImGui_Col_ChildBg()
```

Background of child windows.
## ImGui_Col_DockingEmptyBg
```
integer reaper.ImGui_Col_DockingEmptyBg()
```

Background color for empty node (e.g. CentralNode with no window docked into it).
## ImGui_Col_DockingPreview
```
integer reaper.ImGui_Col_DockingPreview()
```

Preview overlay color when about to docking something.
## ImGui_Col_DragDropTarget
```
integer reaper.ImGui_Col_DragDropTarget()
```

Rectangle highlighting a drop target
## ImGui_Col_FrameBg
```
integer reaper.ImGui_Col_FrameBg()
```

Background of checkbox, radio button, plot, slider, text input.
## ImGui_Col_FrameBgActive
```
integer reaper.ImGui_Col_FrameBgActive()
```

No description available.
## ImGui_Col_FrameBgHovered
```
integer reaper.ImGui_Col_FrameBgHovered()
```

No description available.
## ImGui_Col_Header
```
integer reaper.ImGui_Col_Header()
```

Header* colors are used for CollapsingHeader, TreeNode, Selectable, MenuItem.
## ImGui_Col_HeaderActive
```
integer reaper.ImGui_Col_HeaderActive()
```

No description available.
## ImGui_Col_HeaderHovered
```
integer reaper.ImGui_Col_HeaderHovered()
```

No description available.
## ImGui_Col_MenuBarBg
```
integer reaper.ImGui_Col_MenuBarBg()
```

No description available.
## ImGui_Col_ModalWindowDimBg
```
integer reaper.ImGui_Col_ModalWindowDimBg()
```

Darken/colorize entire screen behind a modal window, when one is active.
## ImGui_Col_NavHighlight
```
integer reaper.ImGui_Col_NavHighlight()
```

Gamepad/keyboard: current highlighted item.
## ImGui_Col_NavWindowingDimBg
```
integer reaper.ImGui_Col_NavWindowingDimBg()
```

Darken/colorize entire screen behind the CTRL+TAB window list, when active.
## ImGui_Col_NavWindowingHighlight
```
integer reaper.ImGui_Col_NavWindowingHighlight()
```

Highlight window when using CTRL+TAB.
## ImGui_Col_PlotHistogram
```
integer reaper.ImGui_Col_PlotHistogram()
```

No description available.
## ImGui_Col_PlotHistogramHovered
```
integer reaper.ImGui_Col_PlotHistogramHovered()
```

No description available.
## ImGui_Col_PlotLines
```
integer reaper.ImGui_Col_PlotLines()
```

No description available.
## ImGui_Col_PlotLinesHovered
```
integer reaper.ImGui_Col_PlotLinesHovered()
```

No description available.
## ImGui_Col_PopupBg
```
integer reaper.ImGui_Col_PopupBg()
```

Background of popups, menus, tooltips windows.
## ImGui_Col_ResizeGrip
```
integer reaper.ImGui_Col_ResizeGrip()
```

Resize grip in lower-right and lower-left corners of windows.
## ImGui_Col_ResizeGripActive
```
integer reaper.ImGui_Col_ResizeGripActive()
```

No description available.
## ImGui_Col_ResizeGripHovered
```
integer reaper.ImGui_Col_ResizeGripHovered()
```

No description available.
## ImGui_Col_ScrollbarBg
```
integer reaper.ImGui_Col_ScrollbarBg()
```

No description available.
## ImGui_Col_ScrollbarGrab
```
integer reaper.ImGui_Col_ScrollbarGrab()
```

No description available.
## ImGui_Col_ScrollbarGrabActive
```
integer reaper.ImGui_Col_ScrollbarGrabActive()
```

No description available.
## ImGui_Col_ScrollbarGrabHovered
```
integer reaper.ImGui_Col_ScrollbarGrabHovered()
```

No description available.
## ImGui_Col_Separator
```
integer reaper.ImGui_Col_Separator()
```

No description available.
## ImGui_Col_SeparatorActive
```
integer reaper.ImGui_Col_SeparatorActive()
```

No description available.
## ImGui_Col_SeparatorHovered
```
integer reaper.ImGui_Col_SeparatorHovered()
```

No description available.
## ImGui_Col_SliderGrab
```
integer reaper.ImGui_Col_SliderGrab()
```

No description available.
## ImGui_Col_SliderGrabActive
```
integer reaper.ImGui_Col_SliderGrabActive()
```

No description available.
## ImGui_Col_Tab
```
integer reaper.ImGui_Col_Tab()
```

Tab background, when tab-bar is focused & tab is unselected
## ImGui_Col_TabDimmed
```
integer reaper.ImGui_Col_TabDimmed()
```

Tab background, when tab-bar is unfocused & tab is unselected
## ImGui_Col_TabDimmedSelected
```
integer reaper.ImGui_Col_TabDimmedSelected()
```

Tab background, when tab-bar is unfocused & tab is selected
## ImGui_Col_TabDimmedSelectedOverline
```
integer reaper.ImGui_Col_TabDimmedSelectedOverline()
```

Horizontal overline, when tab-bar is unfocused & tab is selected
## ImGui_Col_TabHovered
```
integer reaper.ImGui_Col_TabHovered()
```

Tab background, when hovered
## ImGui_Col_TabSelected
```
integer reaper.ImGui_Col_TabSelected()
```

Tab background, when tab-bar is focused & tab is selected
## ImGui_Col_TabSelectedOverline
```
integer reaper.ImGui_Col_TabSelectedOverline()
```

Tab horizontal overline, when tab-bar is focused & tab is selected
## ImGui_Col_TableBorderLight
```
integer reaper.ImGui_Col_TableBorderLight()
```

Table inner borders (prefer using Alpha=1.0 here).
## ImGui_Col_TableBorderStrong
```
integer reaper.ImGui_Col_TableBorderStrong()
```

Table outer and header borders (prefer using Alpha=1.0 here).
## ImGui_Col_TableHeaderBg
```
integer reaper.ImGui_Col_TableHeaderBg()
```

Table header background.
## ImGui_Col_TableRowBg
```
integer reaper.ImGui_Col_TableRowBg()
```

Table row background (even rows).
## ImGui_Col_TableRowBgAlt
```
integer reaper.ImGui_Col_TableRowBgAlt()
```

Table row background (odd rows).
## ImGui_Col_Text
```
integer reaper.ImGui_Col_Text()
```

No description available.
## ImGui_Col_TextDisabled
```
integer reaper.ImGui_Col_TextDisabled()
```

No description available.
## ImGui_Col_TextSelectedBg
```
integer reaper.ImGui_Col_TextSelectedBg()
```

No description available.
## ImGui_Col_TitleBg
```
integer reaper.ImGui_Col_TitleBg()
```

Title bar
## ImGui_Col_TitleBgActive
```
integer reaper.ImGui_Col_TitleBgActive()
```

Title bar when focused
## ImGui_Col_TitleBgCollapsed
```
integer reaper.ImGui_Col_TitleBgCollapsed()
```

Title bar when collapsed
## ImGui_Col_WindowBg
```
integer reaper.ImGui_Col_WindowBg()
```

Background of normal windows. See also WindowFlags_NoBackground.
## ImGui_CollapsingHeader
```
boolean retval, optional boolean p_visible = reaper.ImGui_CollapsingHeader(ImGui_Context ctx, string label, optional boolean p_visible, optional integer flagsIn)
```

Returns true when opened but do not indent nor push into the ID stack
(because of the TreeNodeFlags_NoTreePushOnOpen flag).
## ImGui_ColorButton
```
boolean reaper.ImGui_ColorButton(ImGui_Context ctx, string desc_id, integer col_rgba, optional integer flagsIn, optional number size_wIn, optional number size_hIn)
```

Display a color square/button, hover for details, return true when pressed.
Color is in 0xRRGGBBAA or, if ColorEditFlags_NoAlpha is set, 0xRRGGBB.
## ImGui_ColorConvertDouble4ToU32
```
integer reaper.ImGui_ColorConvertDouble4ToU32(number r, number g, number b, number a)
```

Pack 0..1 RGBA values into a 32-bit integer (0xRRGGBBAA).
## ImGui_ColorConvertHSVtoRGB
```
number r, number g, number b = reaper.ImGui_ColorConvertHSVtoRGB(number h, number s, number v)
```

Convert HSV values (0..1) into RGB (0..1).
## ImGui_ColorConvertNative
```
integer reaper.ImGui_ColorConvertNative(integer rgb)
```

Convert a native color coming from REAPER or 0xRRGGBB to native.
This swaps the red and blue channels on Windows.
## ImGui_ColorConvertRGBtoHSV
```
number h, number s, number v = reaper.ImGui_ColorConvertRGBtoHSV(number r, number g, number b)
```

Convert RGB values (0..1) into HSV (0..1).
## ImGui_ColorConvertU32ToDouble4
```
number r, number g, number b, number a = reaper.ImGui_ColorConvertU32ToDouble4(integer rgba)
```

Unpack a 32-bit integer (0xRRGGBBAA) into separate RGBA values (0..1).
## ImGui_ColorEdit3
```
boolean retval, integer col_rgb = reaper.ImGui_ColorEdit3(ImGui_Context ctx, string label, integer col_rgb, optional integer flagsIn)
```

Color is in 0xXXRRGGBB. XX is ignored and will not be modified.
## ImGui_ColorEdit4
```
boolean retval, integer col_rgba = reaper.ImGui_ColorEdit4(ImGui_Context ctx, string label, integer col_rgba, optional integer flagsIn)
```

Color is in 0xRRGGBBAA or, if ColorEditFlags_NoAlpha is set, 0xXXRRGGBB
(XX is ignored and will not be modified).
## ImGui_ColorEditFlags_AlphaBar
```
integer reaper.ImGui_ColorEditFlags_AlphaBar()
```

ColorEdit, ColorPicker: show vertical alpha bar/gradient in picker.
## ImGui_ColorEditFlags_AlphaPreview
```
integer reaper.ImGui_ColorEditFlags_AlphaPreview()
```

ColorEdit, ColorPicker, ColorButton: display preview as a transparent color over a checkerboard, instead of opaque.
## ImGui_ColorEditFlags_AlphaPreviewHalf
```
integer reaper.ImGui_ColorEditFlags_AlphaPreviewHalf()
```

ColorEdit, ColorPicker, ColorButton: display half opaque / half checkerboard, instead of opaque.
## ImGui_ColorEditFlags_DisplayHSV
```
integer reaper.ImGui_ColorEditFlags_DisplayHSV()
```

ColorEdit: override _display_ type to HSV. ColorPicker: select any combination using one or more of RGB/HSV/Hex.
## ImGui_ColorEditFlags_DisplayHex
```
integer reaper.ImGui_ColorEditFlags_DisplayHex()
```

ColorEdit: override _display_ type to Hex. ColorPicker: select any combination using one or more of RGB/HSV/Hex.
## ImGui_ColorEditFlags_DisplayRGB
```
integer reaper.ImGui_ColorEditFlags_DisplayRGB()
```

ColorEdit: override _display_ type to RGB. ColorPicker: select any combination using one or more of RGB/HSV/Hex.
## ImGui_ColorEditFlags_Float
```
integer reaper.ImGui_ColorEditFlags_Float()
```

ColorEdit, ColorPicker, ColorButton: _display_ values formatted as 0.0..1.0 floats instead of 0..255 integers. No round-trip of value via integers.
## ImGui_ColorEditFlags_InputHSV
```
integer reaper.ImGui_ColorEditFlags_InputHSV()
```

ColorEdit, ColorPicker: input and output data in HSV format.
## ImGui_ColorEditFlags_InputRGB
```
integer reaper.ImGui_ColorEditFlags_InputRGB()
```

ColorEdit, ColorPicker: input and output data in RGB format.
## ImGui_ColorEditFlags_NoAlpha
```
integer reaper.ImGui_ColorEditFlags_NoAlpha()
```

ColorEdit, ColorPicker, ColorButton: ignore Alpha component (will only read 3 components from the input pointer).
## ImGui_ColorEditFlags_NoBorder
```
integer reaper.ImGui_ColorEditFlags_NoBorder()
```

ColorButton: disable border (which is enforced by default).
## ImGui_ColorEditFlags_NoDragDrop
```
integer reaper.ImGui_ColorEditFlags_NoDragDrop()
```

ColorEdit: disable drag and drop target. ColorButton: disable drag and drop source.
## ImGui_ColorEditFlags_NoInputs
```
integer reaper.ImGui_ColorEditFlags_NoInputs()
```

ColorEdit, ColorPicker: disable inputs sliders/text widgets (e.g. to show only the small preview color square).
## ImGui_ColorEditFlags_NoLabel
```
integer reaper.ImGui_ColorEditFlags_NoLabel()
```

ColorEdit, ColorPicker: disable display of inline text label (the label is still forwarded to the tooltip and picker).
## ImGui_ColorEditFlags_NoOptions
```
integer reaper.ImGui_ColorEditFlags_NoOptions()
```

ColorEdit: disable toggling options menu when right-clicking on inputs/small preview.
## ImGui_ColorEditFlags_NoPicker
```
integer reaper.ImGui_ColorEditFlags_NoPicker()
```

ColorEdit: disable picker when clicking on color square.
## ImGui_ColorEditFlags_NoSidePreview
```
integer reaper.ImGui_ColorEditFlags_NoSidePreview()
```

ColorPicker: disable bigger color preview on right side of the picker, use small color square preview instead.
## ImGui_ColorEditFlags_NoSmallPreview
```
integer reaper.ImGui_ColorEditFlags_NoSmallPreview()
```

ColorEdit, ColorPicker: disable color square preview next to the inputs. (e.g. to show only the inputs).
## ImGui_ColorEditFlags_NoTooltip
```
integer reaper.ImGui_ColorEditFlags_NoTooltip()
```

ColorEdit, ColorPicker, ColorButton: disable tooltip when hovering the preview.
## ImGui_ColorEditFlags_None
```
integer reaper.ImGui_ColorEditFlags_None()
```

No description available.
## ImGui_ColorEditFlags_PickerHueBar
```
integer reaper.ImGui_ColorEditFlags_PickerHueBar()
```

ColorPicker: bar for Hue, rectangle for Sat/Value.
## ImGui_ColorEditFlags_PickerHueWheel
```
integer reaper.ImGui_ColorEditFlags_PickerHueWheel()
```

ColorPicker: wheel for Hue, triangle for Sat/Value.
## ImGui_ColorEditFlags_Uint8
```
integer reaper.ImGui_ColorEditFlags_Uint8()
```

ColorEdit, ColorPicker, ColorButton: _display_ values formatted as 0..255.
## ImGui_ColorPicker3
```
boolean retval, integer col_rgb = reaper.ImGui_ColorPicker3(ImGui_Context ctx, string label, integer col_rgb, optional integer flagsIn)
```

Color is in 0xXXRRGGBB. XX is ignored and will not be modified.
## ImGui_ColorPicker4
```
boolean retval, integer col_rgba = reaper.ImGui_ColorPicker4(ImGui_Context ctx, string label, integer col_rgba, optional integer flagsIn, optional integer ref_colIn)
```

No description available.
## ImGui_Combo
```
boolean retval, integer current_item = reaper.ImGui_Combo(ImGui_Context ctx, string label, integer current_item, string items, optional integer popup_max_height_in_itemsIn)
```

Helper over BeginCombo/EndCombo for convenience purpose. Each item must be
null-terminated (requires REAPER v6.44 or newer for EEL and Lua).
## ImGui_ComboFlags_HeightLarge
```
integer reaper.ImGui_ComboFlags_HeightLarge()
```

Max ~20 items visible.
## ImGui_ComboFlags_HeightLargest
```
integer reaper.ImGui_ComboFlags_HeightLargest()
```

As many fitting items as possible.
## ImGui_ComboFlags_HeightRegular
```
integer reaper.ImGui_ComboFlags_HeightRegular()
```

Max ~8 items visible (default).
## ImGui_ComboFlags_HeightSmall
```
integer reaper.ImGui_ComboFlags_HeightSmall()
```

Max ~4 items visible. Tip: If you want your combo popup to be a specific size
you can use SetNextWindowSizeConstraints prior to calling BeginCombo.
## ImGui_ComboFlags_NoArrowButton
```
integer reaper.ImGui_ComboFlags_NoArrowButton()
```

Display on the preview box without the square arrow button.
## ImGui_ComboFlags_NoPreview
```
integer reaper.ImGui_ComboFlags_NoPreview()
```

Display only a square arrow button.
## ImGui_ComboFlags_None
```
integer reaper.ImGui_ComboFlags_None()
```

No description available.
## ImGui_ComboFlags_PopupAlignLeft
```
integer reaper.ImGui_ComboFlags_PopupAlignLeft()
```

Align the popup toward the left by default.
## ImGui_ComboFlags_WidthFitPreview
```
integer reaper.ImGui_ComboFlags_WidthFitPreview()
```

Width dynamically calculated from preview contents.
## ImGui_Cond_Always
```
integer reaper.ImGui_Cond_Always()
```

No condition (always set the variable).
## ImGui_Cond_Appearing
```
integer reaper.ImGui_Cond_Appearing()
```

Set the variable if the object/window is appearing after being hidden/inactive (or the first time).
## ImGui_Cond_FirstUseEver
```
integer reaper.ImGui_Cond_FirstUseEver()
```

Set the variable if the object/window has no persistently saved data (no entry in .ini file).
## ImGui_Cond_Once
```
integer reaper.ImGui_Cond_Once()
```

Set the variable once per runtime session (only the first call will succeed).
## ImGui_ConfigFlags_DockingEnable
```
integer reaper.ImGui_ConfigFlags_DockingEnable()
```

Enable docking functionality.
## ImGui_ConfigFlags_NavEnableKeyboard
```
integer reaper.ImGui_ConfigFlags_NavEnableKeyboard()
```

Master keyboard navigation enable flag. Enable full Tabbing + directional arrows + space/enter to activate.
## ImGui_ConfigFlags_NavEnableSetMousePos
```
integer reaper.ImGui_ConfigFlags_NavEnableSetMousePos()
```

Instruct navigation to move the mouse cursor.
## ImGui_ConfigFlags_NavNoCaptureKeyboard
```
integer reaper.ImGui_ConfigFlags_NavNoCaptureKeyboard()
```

Instruct navigation to not capture global keyboard input when ConfigFlags_NavEnableKeyboard is set (see SetNextFrameWantCaptureKeyboard).
## ImGui_ConfigFlags_NoKeyboard
```
integer reaper.ImGui_ConfigFlags_NoKeyboard()
```

Instruct dear imgui to disable keyboard inputs and interactions.
This is done by ignoring keyboard events and clearing existing states.
## ImGui_ConfigFlags_NoMouse
```
integer reaper.ImGui_ConfigFlags_NoMouse()
```

Instruct dear imgui to disable mouse inputs and interactions
## ImGui_ConfigFlags_NoMouseCursorChange
```
integer reaper.ImGui_ConfigFlags_NoMouseCursorChange()
```

Instruct backend to not alter mouse cursor shape and visibility.
## ImGui_ConfigFlags_NoSavedSettings
```
integer reaper.ImGui_ConfigFlags_NoSavedSettings()
```

Disable state restoration and persistence for the whole context.
## ImGui_ConfigFlags_None
```
integer reaper.ImGui_ConfigFlags_None()
```

No description available.
## ImGui_ConfigVar_DebugBeginReturnValueLoop
```
integer reaper.ImGui_ConfigVar_DebugBeginReturnValueLoop()
```

Some calls to Begin()/BeginChild() will return false.
Will cycle through window depths then repeat. Suggested use: add
"SetConfigVar(ConfigVar_DebugBeginReturnValueLoop(), GetKeyMods() == Mod_Shift"
in your main loop then occasionally press SHIFT.
Windows should be flickering while running.
## ImGui_ConfigVar_DebugBeginReturnValueOnce
```
integer reaper.ImGui_ConfigVar_DebugBeginReturnValueOnce()
```

First-time calls to Begin()/BeginChild() will return false.
**Needs to be set at context startup time** if you don't want to miss windows.
## ImGui_ConfigVar_DockingNoSplit
```
integer reaper.ImGui_ConfigVar_DockingNoSplit()
```

Simplified docking mode: disable window splitting, so docking is limited to merging multiple windows together into tab-bars.
## ImGui_ConfigVar_DockingTransparentPayload
```
integer reaper.ImGui_ConfigVar_DockingTransparentPayload()
```

Make window or viewport transparent when docking and only display docking boxes on the target viewport.
## ImGui_ConfigVar_DockingWithShift
```
integer reaper.ImGui_ConfigVar_DockingWithShift()
```

Enable docking with holding Shift key (reduce visual noise, allows dropping in wider space
## ImGui_ConfigVar_DragClickToInputText
```
integer reaper.ImGui_ConfigVar_DragClickToInputText()
```

Enable turning Drag* widgets into text input with a simple mouse click-release (without moving). Not desirable on devices without a keyboard.
## ImGui_ConfigVar_Flags
```
integer reaper.ImGui_ConfigVar_Flags()
```

ConfigFlags_*
## ImGui_ConfigVar_HoverDelayNormal
```
integer reaper.ImGui_ConfigVar_HoverDelayNormal()
```

Delay for IsItemHovered(HoveredFlags_DelayNormal). Usually used along with ConfigVar_HoverStationaryDelay.
## ImGui_ConfigVar_HoverDelayShort
```
integer reaper.ImGui_ConfigVar_HoverDelayShort()
```

Delay for IsItemHovered(HoveredFlags_DelayShort). Usually used along with ConfigVar_HoverStationaryDelay.
## ImGui_ConfigVar_HoverFlagsForTooltipMouse
```
integer reaper.ImGui_ConfigVar_HoverFlagsForTooltipMouse()
```

Default flags when using IsItemHovered(HoveredFlags_ForTooltip) or BeginItemTooltip()/SetItemTooltip() while using mouse.
## ImGui_ConfigVar_HoverFlagsForTooltipNav
```
integer reaper.ImGui_ConfigVar_HoverFlagsForTooltipNav()
```

Default flags when using IsItemHovered(HoveredFlags_ForTooltip) or BeginItemTooltip()/SetItemTooltip() while using keyboard/gamepad.
## ImGui_ConfigVar_HoverStationaryDelay
```
integer reaper.ImGui_ConfigVar_HoverStationaryDelay()
```

Delay for IsItemHovered(HoveredFlags_Stationary). Time required to consider mouse stationary.
## ImGui_ConfigVar_InputTextCursorBlink
```
integer reaper.ImGui_ConfigVar_InputTextCursorBlink()
```

Enable blinking cursor (optional as some users consider it to be distracting).
## ImGui_ConfigVar_InputTextEnterKeepActive
```
integer reaper.ImGui_ConfigVar_InputTextEnterKeepActive()
```

Pressing Enter will keep item active and select contents (single-line only).
## ImGui_ConfigVar_InputTrickleEventQueue
```
integer reaper.ImGui_ConfigVar_InputTrickleEventQueue()
```

Enable input queue trickling: some types of events submitted during the same frame (e.g. button down + up) will be spread over multiple frames, improving interactions with low framerates.
## ImGui_ConfigVar_KeyRepeatDelay
```
integer reaper.ImGui_ConfigVar_KeyRepeatDelay()
```

When holding a key/button, time before it starts repeating, in seconds (for buttons in Repeat mode, etc.).
## ImGui_ConfigVar_KeyRepeatRate
```
integer reaper.ImGui_ConfigVar_KeyRepeatRate()
```

When holding a key/button, rate at which it repeats, in seconds.
## ImGui_ConfigVar_MacOSXBehaviors
```
integer reaper.ImGui_ConfigVar_MacOSXBehaviors()
```

Enabled by default on macOS. Swap Cmd<>Ctrl keys, OS X style text editing cursor movement using Alt instead of Ctrl, Shortcuts using Cmd/Super instead of Ctrl, Line/Text Start and End using Cmd+Arrows instead of Home/End, Double click selects by word instead of selecting whole text, Multi-selection in lists uses Cmd/Super instead of Ctrl.
## ImGui_ConfigVar_MouseDoubleClickMaxDist
```
integer reaper.ImGui_ConfigVar_MouseDoubleClickMaxDist()
```

Distance threshold to stay in to validate a double-click, in pixels.
## ImGui_ConfigVar_MouseDoubleClickTime
```
integer reaper.ImGui_ConfigVar_MouseDoubleClickTime()
```

Time for a double-click, in seconds.
## ImGui_ConfigVar_MouseDragThreshold
```
integer reaper.ImGui_ConfigVar_MouseDragThreshold()
```

Distance threshold before considering we are dragging.
## ImGui_ConfigVar_ViewportsNoDecoration
```
integer reaper.ImGui_ConfigVar_ViewportsNoDecoration()
```

Disable default OS window decoration. Enabling decoration can create subsequent issues at OS levels (e.g. minimum window size).
## ImGui_ConfigVar_WindowsMoveFromTitleBarOnly
```
integer reaper.ImGui_ConfigVar_WindowsMoveFromTitleBarOnly()
```

Enable allowing to move windows only when clicking on their title bar. Does not apply to windows without a title bar.
## ImGui_ConfigVar_WindowsResizeFromEdges
```
integer reaper.ImGui_ConfigVar_WindowsResizeFromEdges()
```

Enable resizing of windows from their edges and from the lower-left corner.
## ImGui_CreateContext
```
ImGui_Context reaper.ImGui_CreateContext(string label, optional integer config_flagsIn)
```

Create a new ReaImGui context.
The context will remain valid as long as it is used in each defer cycle.
## ImGui_CreateDrawListSplitter
```
ImGui_DrawListSplitter reaper.ImGui_CreateDrawListSplitter(ImGui_DrawList draw_list)
```

No description available.
## ImGui_CreateFont
```
ImGui_Font reaper.ImGui_CreateFont(string family_or_file, integer size, optional integer flagsIn)
```

Load a font matching a font family name or from a font file.
The font will remain valid while it's attached to a context. See Attach.
## ImGui_CreateFontFromMem
```
ImGui_Font reaper.ImGui_CreateFontFromMem(string data, integer size, optional integer flagsIn)
```

Requires REAPER v6.44 or newer for EEL and Lua. Use CreateFont or
explicitely specify data_sz to support older versions.
## ImGui_CreateFunctionFromEEL
```
ImGui_Function reaper.ImGui_CreateFunctionFromEEL(string code)
```

Compile an EEL program.
## ImGui_CreateImage
```
ImGui_Image reaper.ImGui_CreateImage(string file, optional integer flagsIn)
```

The returned object is valid as long as it is used in each defer cycle
unless attached to a context (see Attach).
## ImGui_CreateImageFromLICE
```
ImGui_Image reaper.ImGui_CreateImageFromLICE(LICE_IBitmap bitmap, optional integer flagsIn)
```

Copies pixel data from a LICE bitmap created using JS_LICE_CreateBitmap.
## ImGui_CreateImageFromMem
```
ImGui_Image reaper.ImGui_CreateImageFromMem(string data, optional integer flagsIn)
```

Requires REAPER v6.44 or newer for EEL and Lua. Load from a file using
CreateImage or explicitely specify data_sz to support older versions.
## ImGui_CreateImageSet
```
ImGui_ImageSet = reaper.ImGui_CreateImageSet()
```

No description available.
## ImGui_CreateListClipper
```
ImGui_ListClipper reaper.ImGui_CreateListClipper(ImGui_Context ctx)
```

The returned clipper object is only valid for the given context and is valid
as long as it is used in each defer cycle unless attached (see Attach).
## ImGui_CreateTextFilter
```
ImGui_TextFilter reaper.ImGui_CreateTextFilter(optional string default_filterIn)
```

Valid while used every frame unless attached to a context (see Attach).
## ImGui_DebugFlashStyleColor
```
reaper.ImGui_DebugFlashStyleColor(ImGui_Context ctx, integer idx)
```

No description available.
## ImGui_DebugStartItemPicker
```
reaper.ImGui_DebugStartItemPicker(ImGui_Context ctx)
```

No description available.
## ImGui_DebugTextEncoding
```
reaper.ImGui_DebugTextEncoding(ImGui_Context ctx, string text)
```

Helper tool to diagnose between text encoding issues and font loading issues.
Pass your UTF-8 string and verify that there are correct.
## ImGui_Detach
```
reaper.ImGui_Detach(ImGui_Context ctx, ImGui_Resource obj)
```

Unlink the object's lifetime. Unattached objects are automatically destroyed
when left unused. You may check whether an object has been destroyed using
ValidatePtr.
## ImGui_Dir_Down
```
integer reaper.ImGui_Dir_Down()
```

No description available.
## ImGui_Dir_Left
```
integer reaper.ImGui_Dir_Left()
```

No description available.
## ImGui_Dir_None
```
integer reaper.ImGui_Dir_None()
```

No description available.
## ImGui_Dir_Right
```
integer reaper.ImGui_Dir_Right()
```

No description available.
## ImGui_Dir_Up
```
integer reaper.ImGui_Dir_Up()
```

No description available.
## ImGui_DragDouble
```
boolean retval, number v = reaper.ImGui_DragDouble(ImGui_Context ctx, string label, number v, optional number v_speedIn, optional number v_minIn, optional number v_maxIn, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_DragDouble2
```
boolean retval, number v1, number v2 = reaper.ImGui_DragDouble2(ImGui_Context ctx, string label, number v1, number v2, optional number v_speedIn, optional number v_minIn, optional number v_maxIn, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_DragDouble3
```
boolean retval, number v1, number v2, number v3 = reaper.ImGui_DragDouble3(ImGui_Context ctx, string label, number v1, number v2, number v3, optional number v_speedIn, optional number v_minIn, optional number v_maxIn, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_DragDouble4
```
boolean retval, number v1, number v2, number v3, number v4 = reaper.ImGui_DragDouble4(ImGui_Context ctx, string label, number v1, number v2, number v3, number v4, optional number v_speedIn, optional number v_minIn, optional number v_maxIn, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_DragDoubleN
```
boolean reaper.ImGui_DragDoubleN(ImGui_Context ctx, string label, reaper_array values, optional number speedIn, optional number minIn, optional number maxIn, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_DragDropFlags_AcceptBeforeDelivery
```
integer reaper.ImGui_DragDropFlags_AcceptBeforeDelivery()
```

AcceptDragDropPayload will returns true even before the mouse button is released. You can then check GetDragDropPayload/is_delivery to test if the payload needs to be delivered.
## ImGui_DragDropFlags_AcceptNoDrawDefaultRect
```
integer reaper.ImGui_DragDropFlags_AcceptNoDrawDefaultRect()
```

Do not draw the default highlight rectangle when hovering over target.
## ImGui_DragDropFlags_AcceptNoPreviewTooltip
```
integer reaper.ImGui_DragDropFlags_AcceptNoPreviewTooltip()
```

Request hiding the BeginDragDropSource tooltip from the BeginDragDropTarget site.
## ImGui_DragDropFlags_AcceptPeekOnly
```
integer reaper.ImGui_DragDropFlags_AcceptPeekOnly()
```

For peeking ahead and inspecting the payload before delivery. Equivalent to DragDropFlags_AcceptBeforeDelivery | DragDropFlags_AcceptNoDrawDefaultRect.
## ImGui_DragDropFlags_None
```
integer reaper.ImGui_DragDropFlags_None()
```

No description available.
## ImGui_DragDropFlags_PayloadAutoExpire
```
integer reaper.ImGui_DragDropFlags_PayloadAutoExpire()
```

Automatically expire the payload if the source cease to be submitted (otherwise payloads are persisting while being dragged).
## ImGui_DragDropFlags_SourceAllowNullID
```
integer reaper.ImGui_DragDropFlags_SourceAllowNullID()
```

Allow items such as Text, Image that have no unique identifier to be used as drag source, by manufacturing a temporary identifier based on their window-relative position. This is extremely unusual within the dear imgui ecosystem and so we made it explicit.
## ImGui_DragDropFlags_SourceExtern
```
integer reaper.ImGui_DragDropFlags_SourceExtern()
```

External source (from outside of dear imgui), won't attempt to read current item/window info. Will always return true. Only one Extern source can be active simultaneously.
## ImGui_DragDropFlags_SourceNoDisableHover
```
integer reaper.ImGui_DragDropFlags_SourceNoDisableHover()
```

By default, when dragging we clear data so that IsItemHovered will return false, to avoid subsequent user code submitting tooltips. This flag disables this behavior so you can still call IsItemHovered on the source item.
## ImGui_DragDropFlags_SourceNoHoldToOpenOthers
```
integer reaper.ImGui_DragDropFlags_SourceNoHoldToOpenOthers()
```

Disable the behavior that allows to open tree nodes and collapsing header by holding over them while dragging a source item.
## ImGui_DragDropFlags_SourceNoPreviewTooltip
```
integer reaper.ImGui_DragDropFlags_SourceNoPreviewTooltip()
```

By default, a successful call to BeginDragDropSource opens a tooltip so you can display a preview or description of the source contents. This flag disables this behavior.
## ImGui_DragFloatRange2
```
boolean retval, number v_current_min, number v_current_max = reaper.ImGui_DragFloatRange2(ImGui_Context ctx, string label, number v_current_min, number v_current_max, optional number v_speedIn, optional number v_minIn, optional number v_maxIn, optional string formatIn, optional string format_maxIn, optional integer flagsIn)
```

No description available.
## ImGui_DragInt
```
boolean retval, integer v = reaper.ImGui_DragInt(ImGui_Context ctx, string label, integer v, optional number v_speedIn, optional integer v_minIn, optional integer v_maxIn, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_DragInt2
```
boolean retval, integer v1, integer v2 = reaper.ImGui_DragInt2(ImGui_Context ctx, string label, integer v1, integer v2, optional number v_speedIn, optional integer v_minIn, optional integer v_maxIn, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_DragInt3
```
boolean retval, integer v1, integer v2, integer v3 = reaper.ImGui_DragInt3(ImGui_Context ctx, string label, integer v1, integer v2, integer v3, optional number v_speedIn, optional integer v_minIn, optional integer v_maxIn, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_DragInt4
```
boolean retval, integer v1, integer v2, integer v3, integer v4 = reaper.ImGui_DragInt4(ImGui_Context ctx, string label, integer v1, integer v2, integer v3, integer v4, optional number v_speedIn, optional integer v_minIn, optional integer v_maxIn, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_DragIntRange2
```
boolean retval, integer v_current_min, integer v_current_max = reaper.ImGui_DragIntRange2(ImGui_Context ctx, string label, integer v_current_min, integer v_current_max, optional number v_speedIn, optional integer v_minIn, optional integer v_maxIn, optional string formatIn, optional string format_maxIn, optional integer flagsIn)
```

No description available.
## ImGui_DrawFlags_Closed
```
integer reaper.ImGui_DrawFlags_Closed()
```

DrawList_PathStroke, DrawList_AddPolyline: specify that shape should be closed (Important: this is always == 1 for legacy reason).
## ImGui_DrawFlags_None
```
integer reaper.ImGui_DrawFlags_None()
```

No description available.
## ImGui_DrawFlags_RoundCornersAll
```
integer reaper.ImGui_DrawFlags_RoundCornersAll()
```

No description available.
## ImGui_DrawFlags_RoundCornersBottom
```
integer reaper.ImGui_DrawFlags_RoundCornersBottom()
```

No description available.
## ImGui_DrawFlags_RoundCornersBottomLeft
```
integer reaper.ImGui_DrawFlags_RoundCornersBottomLeft()
```

DrawList_AddRect, DrawList_AddRectFilled, DrawList_PathRect: enable rounding bottom-left corner only (when rounding > 0.0, we default to all corners).
## ImGui_DrawFlags_RoundCornersBottomRight
```
integer reaper.ImGui_DrawFlags_RoundCornersBottomRight()
```

DrawList_AddRect, DrawList_AddRectFilled, DrawList_PathRect: enable rounding bottom-right corner only (when rounding > 0.0, we default to all corners).
## ImGui_DrawFlags_RoundCornersLeft
```
integer reaper.ImGui_DrawFlags_RoundCornersLeft()
```

No description available.
## ImGui_DrawFlags_RoundCornersNone
```
integer reaper.ImGui_DrawFlags_RoundCornersNone()
```

DrawList_AddRect, DrawList_AddRectFilled, DrawList_PathRect: disable rounding on all corners (when rounding > 0.0). This is NOT zero, NOT an implicit flag!.
## ImGui_DrawFlags_RoundCornersRight
```
integer reaper.ImGui_DrawFlags_RoundCornersRight()
```

No description available.
## ImGui_DrawFlags_RoundCornersTop
```
integer reaper.ImGui_DrawFlags_RoundCornersTop()
```

No description available.
## ImGui_DrawFlags_RoundCornersTopLeft
```
integer reaper.ImGui_DrawFlags_RoundCornersTopLeft()
```

DrawList_AddRect, DrawList_AddRectFilled, DrawList_PathRect: enable rounding top-left corner only (when rounding > 0.0, we default to all corners).
## ImGui_DrawFlags_RoundCornersTopRight
```
integer reaper.ImGui_DrawFlags_RoundCornersTopRight()
```

DrawList_AddRect, DrawList_AddRectFilled, DrawList_PathRect: enable rounding top-right corner only (when rounding > 0.0, we default to all corners).
## ImGui_DrawListSplitter_Clear
```
reaper.ImGui_DrawListSplitter_Clear(ImGui_DrawListSplitter splitter)
```

No description available.
## ImGui_DrawListSplitter_Merge
```
reaper.ImGui_DrawListSplitter_Merge(ImGui_DrawListSplitter splitter)
```

No description available.
## ImGui_DrawListSplitter_SetCurrentChannel
```
reaper.ImGui_DrawListSplitter_SetCurrentChannel(ImGui_DrawListSplitter splitter, integer channel_idx)
```

No description available.
## ImGui_DrawListSplitter_Split
```
reaper.ImGui_DrawListSplitter_Split(ImGui_DrawListSplitter splitter, integer count)
```

No description available.
## ImGui_DrawList_AddBezierCubic
```
reaper.ImGui_DrawList_AddBezierCubic(ImGui_DrawList draw_list, number p1_x, number p1_y, number p2_x, number p2_y, number p3_x, number p3_y, number p4_x, number p4_y, integer col_rgba, number thickness, optional integer num_segmentsIn)
```

Cubic Bezier (4 control points)
## ImGui_DrawList_AddBezierQuadratic
```
reaper.ImGui_DrawList_AddBezierQuadratic(ImGui_DrawList draw_list, number p1_x, number p1_y, number p2_x, number p2_y, number p3_x, number p3_y, integer col_rgba, number thickness, optional integer num_segmentsIn)
```

Quadratic Bezier (3 control points)
## ImGui_DrawList_AddCircle
```
reaper.ImGui_DrawList_AddCircle(ImGui_DrawList draw_list, number center_x, number center_y, number radius, integer col_rgba, optional integer num_segmentsIn, optional number thicknessIn)
```

Use "num_segments == 0" to automatically calculate tessellation (preferred).
## ImGui_DrawList_AddCircleFilled
```
reaper.ImGui_DrawList_AddCircleFilled(ImGui_DrawList draw_list, number center_x, number center_y, number radius, integer col_rgba, optional integer num_segmentsIn)
```

Use "num_segments == 0" to automatically calculate tessellation (preferred).
## ImGui_DrawList_AddConcavePolyFilled
```
reaper.ImGui_DrawList_AddConcavePolyFilled(ImGui_DrawList draw_list, reaper_array points, integer col_rgba)
```

Concave polygon fill is more expensive than convex one: it has O(N^2) complexity.
## ImGui_DrawList_AddConvexPolyFilled
```
reaper.ImGui_DrawList_AddConvexPolyFilled(ImGui_DrawList draw_list, reaper_array points, integer col_rgba)
```

Note: Anti-aliased filling requires points to be in clockwise order.
## ImGui_DrawList_AddEllipse
```
reaper.ImGui_DrawList_AddEllipse(ImGui_DrawList draw_list, number center_x, number center_y, number radius_x, number radius_y, integer col_rgba, optional number rotIn, optional integer num_segmentsIn, optional number thicknessIn)
```

No description available.
## ImGui_DrawList_AddEllipseFilled
```
reaper.ImGui_DrawList_AddEllipseFilled(ImGui_DrawList draw_list, number center_x, number center_y, number radius_x, number radius_y, integer col_rgba, optional number rotIn, optional integer num_segmentsIn)
```

No description available.
## ImGui_DrawList_AddImage
```
reaper.ImGui_DrawList_AddImage(ImGui_DrawList draw_list, ImGui_Image image, number p_min_x, number p_min_y, number p_max_x, number p_max_y, optional number uv_min_xIn, optional number uv_min_yIn, optional number uv_max_xIn, optional number uv_max_yIn, optional integer col_rgbaIn)
```

No description available.
## ImGui_DrawList_AddImageQuad
```
reaper.ImGui_DrawList_AddImageQuad(ImGui_DrawList draw_list, ImGui_Image image, number p1_x, number p1_y, number p2_x, number p2_y, number p3_x, number p3_y, number p4_x, number p4_y, optional number uv1_xIn, optional number uv1_yIn, optional number uv2_xIn, optional number uv2_yIn, optional number uv3_xIn, optional number uv3_yIn, optional number uv4_xIn, optional number uv4_yIn, optional integer col_rgbaIn)
```

No description available.
## ImGui_DrawList_AddImageRounded
```
reaper.ImGui_DrawList_AddImageRounded(ImGui_DrawList draw_list, ImGui_Image image, number p_min_x, number p_min_y, number p_max_x, number p_max_y, number uv_min_x, number uv_min_y, number uv_max_x, number uv_max_y, integer col_rgba, number rounding, optional integer flagsIn)
```

No description available.
## ImGui_DrawList_AddLine
```
reaper.ImGui_DrawList_AddLine(ImGui_DrawList draw_list, number p1_x, number p1_y, number p2_x, number p2_y, integer col_rgba, optional number thicknessIn)
```

No description available.
## ImGui_DrawList_AddNgon
```
reaper.ImGui_DrawList_AddNgon(ImGui_DrawList draw_list, number center_x, number center_y, number radius, integer col_rgba, integer num_segments, optional number thicknessIn)
```

No description available.
## ImGui_DrawList_AddNgonFilled
```
reaper.ImGui_DrawList_AddNgonFilled(ImGui_DrawList draw_list, number center_x, number center_y, number radius, integer col_rgba, integer num_segments)
```

No description available.
## ImGui_DrawList_AddPolyline
```
reaper.ImGui_DrawList_AddPolyline(ImGui_DrawList draw_list, reaper_array points, integer col_rgba, integer flags, number thickness)
```

Points is a list of x,y coordinates.
## ImGui_DrawList_AddQuad
```
reaper.ImGui_DrawList_AddQuad(ImGui_DrawList draw_list, number p1_x, number p1_y, number p2_x, number p2_y, number p3_x, number p3_y, number p4_x, number p4_y, integer col_rgba, optional number thicknessIn)
```

No description available.
## ImGui_DrawList_AddQuadFilled
```
reaper.ImGui_DrawList_AddQuadFilled(ImGui_DrawList draw_list, number p1_x, number p1_y, number p2_x, number p2_y, number p3_x, number p3_y, number p4_x, number p4_y, integer col_rgba)
```

No description available.
## ImGui_DrawList_AddRect
```
reaper.ImGui_DrawList_AddRect(ImGui_DrawList draw_list, number p_min_x, number p_min_y, number p_max_x, number p_max_y, integer col_rgba, optional number roundingIn, optional integer flagsIn, optional number thicknessIn)
```

No description available.
## ImGui_DrawList_AddRectFilled
```
reaper.ImGui_DrawList_AddRectFilled(ImGui_DrawList draw_list, number p_min_x, number p_min_y, number p_max_x, number p_max_y, integer col_rgba, optional number roundingIn, optional integer flagsIn)
```

No description available.
## ImGui_DrawList_AddRectFilledMultiColor
```
reaper.ImGui_DrawList_AddRectFilledMultiColor(ImGui_DrawList draw_list, number p_min_x, number p_min_y, number p_max_x, number p_max_y, integer col_upr_left, integer col_upr_right, integer col_bot_right, integer col_bot_left)
```

No description available.
## ImGui_DrawList_AddText
```
reaper.ImGui_DrawList_AddText(ImGui_DrawList draw_list, number x, number y, integer col_rgba, string text)
```

No description available.
## ImGui_DrawList_AddTextEx
```
reaper.ImGui_DrawList_AddTextEx(ImGui_DrawList draw_list, ImGui_Font font, number font_size, number pos_x, number pos_y, integer col_rgba, string text, optional number wrap_widthIn, optional number cpu_fine_clip_rect_min_xIn, optional number cpu_fine_clip_rect_min_yIn, optional number cpu_fine_clip_rect_max_xIn, optional number cpu_fine_clip_rect_max_yIn)
```

The last pushed font is used if font is nil.
The size of the last pushed font is used if font_size is 0.
cpu_fine_clip_rect_* only takes effect if all four are non-nil.
## ImGui_DrawList_AddTriangle
```
reaper.ImGui_DrawList_AddTriangle(ImGui_DrawList draw_list, number p1_x, number p1_y, number p2_x, number p2_y, number p3_x, number p3_y, integer col_rgba, optional number thicknessIn)
```

No description available.
## ImGui_DrawList_AddTriangleFilled
```
reaper.ImGui_DrawList_AddTriangleFilled(ImGui_DrawList draw_list, number p1_x, number p1_y, number p2_x, number p2_y, number p3_x, number p3_y, integer col_rgba)
```

No description available.
## ImGui_DrawList_PathArcTo
```
reaper.ImGui_DrawList_PathArcTo(ImGui_DrawList draw_list, number center_x, number center_y, number radius, number a_min, number a_max, optional integer num_segmentsIn)
```

No description available.
## ImGui_DrawList_PathArcToFast
```
reaper.ImGui_DrawList_PathArcToFast(ImGui_DrawList draw_list, number center_x, number center_y, number radius, integer a_min_of_12, integer a_max_of_12)
```

Use precomputed angles for a 12 steps circle.
## ImGui_DrawList_PathBezierCubicCurveTo
```
reaper.ImGui_DrawList_PathBezierCubicCurveTo(ImGui_DrawList draw_list, number p2_x, number p2_y, number p3_x, number p3_y, number p4_x, number p4_y, optional integer num_segmentsIn)
```

Cubic Bezier (4 control points)
## ImGui_DrawList_PathBezierQuadraticCurveTo
```
reaper.ImGui_DrawList_PathBezierQuadraticCurveTo(ImGui_DrawList draw_list, number p2_x, number p2_y, number p3_x, number p3_y, optional integer num_segmentsIn)
```

Quadratic Bezier (3 control points)
## ImGui_DrawList_PathClear
```
reaper.ImGui_DrawList_PathClear(ImGui_DrawList draw_list)
```

No description available.
## ImGui_DrawList_PathEllipticalArcTo
```
reaper.ImGui_DrawList_PathEllipticalArcTo(ImGui_DrawList draw_list, number center_x, number center_y, number radius_x, number radius_y, number rot, number a_min, number a_max, optional integer num_segmentsIn)
```

Ellipse
## ImGui_DrawList_PathFillConcave
```
reaper.ImGui_DrawList_PathFillConcave(ImGui_DrawList draw_list, integer col_rgba)
```

No description available.
## ImGui_DrawList_PathFillConvex
```
reaper.ImGui_DrawList_PathFillConvex(ImGui_DrawList draw_list, integer col_rgba)
```

No description available.
## ImGui_DrawList_PathLineTo
```
reaper.ImGui_DrawList_PathLineTo(ImGui_DrawList draw_list, number pos_x, number pos_y)
```

No description available.
## ImGui_DrawList_PathRect
```
reaper.ImGui_DrawList_PathRect(ImGui_DrawList draw_list, number rect_min_x, number rect_min_y, number rect_max_x, number rect_max_y, optional number roundingIn, optional integer flagsIn)
```

No description available.
## ImGui_DrawList_PathStroke
```
reaper.ImGui_DrawList_PathStroke(ImGui_DrawList draw_list, integer col_rgba, optional integer flagsIn, optional number thicknessIn)
```

No description available.
## ImGui_DrawList_PopClipRect
```
reaper.ImGui_DrawList_PopClipRect(ImGui_DrawList draw_list)
```

See DrawList_PushClipRect
## ImGui_DrawList_PushClipRect
```
reaper.ImGui_DrawList_PushClipRect(ImGui_DrawList draw_list, number clip_rect_min_x, number clip_rect_min_y, number clip_rect_max_x, number clip_rect_max_y, optional boolean intersect_with_current_clip_rectIn)
```

Render-level scissoring. Prefer using higher-level PushClipRect to affect
logic (hit-testing and widget culling).
## ImGui_DrawList_PushClipRectFullScreen
```
reaper.ImGui_DrawList_PushClipRectFullScreen(ImGui_DrawList draw_list)
```

No description available.
## ImGui_Dummy
```
reaper.ImGui_Dummy(ImGui_Context ctx, number size_w, number size_h)
```

Add a dummy item of given size. unlike InvisibleButton, Dummy() won't take the
mouse click or be navigable into.
## ImGui_End
```
reaper.ImGui_End(ImGui_Context ctx)
```

Pop window from the stack. See Begin.
## ImGui_EndChild
```
reaper.ImGui_EndChild(ImGui_Context ctx)
```

See BeginChild.
## ImGui_EndCombo
```
reaper.ImGui_EndCombo(ImGui_Context ctx)
```

Only call EndCombo() if BeginCombo returns true!
## ImGui_EndDisabled
```
reaper.ImGui_EndDisabled(ImGui_Context ctx)
```

See BeginDisabled.
## ImGui_EndDragDropSource
```
reaper.ImGui_EndDragDropSource(ImGui_Context ctx)
```

Only call EndDragDropSource() if BeginDragDropSource returns true!
## ImGui_EndDragDropTarget
```
reaper.ImGui_EndDragDropTarget(ImGui_Context ctx)
```

Only call EndDragDropTarget() if BeginDragDropTarget returns true!
## ImGui_EndGroup
```
reaper.ImGui_EndGroup(ImGui_Context ctx)
```

Unlock horizontal starting position + capture the whole group bounding box
into one "item" (so you can use IsItemHovered or layout primitives such as
SameLine on whole group, etc.).
## ImGui_EndListBox
```
reaper.ImGui_EndListBox(ImGui_Context ctx)
```

Only call EndListBox() if BeginListBox returned true!
## ImGui_EndMenu
```
reaper.ImGui_EndMenu(ImGui_Context ctx)
```

Only call EndMenu() if BeginMenu returns true!
## ImGui_EndMenuBar
```
reaper.ImGui_EndMenuBar(ImGui_Context ctx)
```

Only call EndMenuBar if BeginMenuBar returns true!
## ImGui_EndPopup
```
reaper.ImGui_EndPopup(ImGui_Context ctx)
```

Only call EndPopup() if BeginPopup*() returns true!
## ImGui_EndTabBar
```
reaper.ImGui_EndTabBar(ImGui_Context ctx)
```

Only call EndTabBar() if BeginTabBar() returns true!
## ImGui_EndTabItem
```
reaper.ImGui_EndTabItem(ImGui_Context ctx)
```

Only call EndTabItem() if BeginTabItem() returns true!
## ImGui_EndTable
```
reaper.ImGui_EndTable(ImGui_Context ctx)
```

Only call EndTable() if BeginTable() returns true!
## ImGui_EndTooltip
```
reaper.ImGui_EndTooltip(ImGui_Context ctx)
```

Only call EndTooltip() if BeginTooltip()/BeginItemTooltip() returns true.
## ImGui_FocusedFlags_AnyWindow
```
integer reaper.ImGui_FocusedFlags_AnyWindow()
```

Return true if any window is focused.
## ImGui_FocusedFlags_ChildWindows
```
integer reaper.ImGui_FocusedFlags_ChildWindows()
```

Return true if any children of the window is focused.
## ImGui_FocusedFlags_DockHierarchy
```
integer reaper.ImGui_FocusedFlags_DockHierarchy()
```

Consider docking hierarchy (treat dockspace host as parent of docked window) (when used with _ChildWindows or _RootWindow).
## ImGui_FocusedFlags_NoPopupHierarchy
```
integer reaper.ImGui_FocusedFlags_NoPopupHierarchy()
```

Do not consider popup hierarchy (do not treat popup emitter as parent of popup) (when used with _ChildWindows or _RootWindow).
## ImGui_FocusedFlags_None
```
integer reaper.ImGui_FocusedFlags_None()
```

No description available.
## ImGui_FocusedFlags_RootAndChildWindows
```
integer reaper.ImGui_FocusedFlags_RootAndChildWindows()
```

FocusedFlags_RootWindow | FocusedFlags_ChildWindows
## ImGui_FocusedFlags_RootWindow
```
integer reaper.ImGui_FocusedFlags_RootWindow()
```

Test from root window (top most parent of the current hierarchy).
## ImGui_FontFlags_Bold
```
integer reaper.ImGui_FontFlags_Bold()
```

No description available.
## ImGui_FontFlags_Italic
```
integer reaper.ImGui_FontFlags_Italic()
```

No description available.
## ImGui_FontFlags_None
```
integer reaper.ImGui_FontFlags_None()
```

No description available.
## ImGui_Function_Execute
```
reaper.ImGui_Function_Execute(ImGui_Function func)
```

No description available.
## ImGui_Function_GetValue
```
number reaper.ImGui_Function_GetValue(ImGui_Function func, string name)
```

No description available.
## ImGui_Function_GetValue_Array
```
reaper.ImGui_Function_GetValue_Array(ImGui_Function func, string name, reaper_array values)
```

Copy the values in the function's memory starting at the address stored
in the given variable into the array.
## ImGui_Function_GetValue_String
```
string value = reaper.ImGui_Function_GetValue_String(ImGui_Function func, string name)
```

Read from a string slot or a named string (when name starts with a `#`).
## ImGui_Function_SetValue
```
reaper.ImGui_Function_SetValue(ImGui_Function func, string name, number value)
```

No description available.
## ImGui_Function_SetValue_Array
```
reaper.ImGui_Function_SetValue_Array(ImGui_Function func, string name, reaper_array values)
```

Copy the values in the array to the function's memory at the address stored
in the given variable.
## ImGui_Function_SetValue_String
```
reaper.ImGui_Function_SetValue_String(ImGui_Function func, string name, string value)
```

Write to a string slot or a named string (when name starts with a `#`).
## ImGui_GetBackgroundDrawList
```
ImGui_DrawList reaper.ImGui_GetBackgroundDrawList(ImGui_Context ctx)
```

This draw list will be the first rendering one. Useful to quickly draw
shapes/text behind dear imgui contents.
## ImGui_GetBuiltinPath
```
string reaper.ImGui_GetBuiltinPath()
```

Returns the path to the directory containing imgui.lua, imgui.py and gfx2imgui.lua.
## ImGui_GetClipboardText
```
string reaper.ImGui_GetClipboardText(ImGui_Context ctx)
```

No description available.
## ImGui_GetColor
```
integer reaper.ImGui_GetColor(ImGui_Context ctx, integer idx, optional number alpha_mulIn)
```

Retrieve given style color with style alpha applied and optional extra alpha
multiplier, packed as a 32-bit value (RGBA). See Col_* for available style colors.
## ImGui_GetColorEx
```
integer reaper.ImGui_GetColorEx(ImGui_Context ctx, integer col_rgba, optional number alpha_mulIn)
```

Retrieve given color with style alpha applied, packed as a 32-bit value (RGBA).
## ImGui_GetConfigVar
```
number reaper.ImGui_GetConfigVar(ImGui_Context ctx, integer var_idx)
```

No description available.
## ImGui_GetContentRegionAvail
```
number x, number y = reaper.ImGui_GetContentRegionAvail(ImGui_Context ctx)
```

== GetContentRegionMax() - GetCursorPos()
## ImGui_GetContentRegionMax
```
number x, number y = reaper.ImGui_GetContentRegionMax(ImGui_Context ctx)
```

Current content boundaries (typically window boundaries including scrolling,
or current column boundaries), in windows coordinates.
## ImGui_GetCursorPos
```
number x, number y = reaper.ImGui_GetCursorPos(ImGui_Context ctx)
```

Cursor position in window
## ImGui_GetCursorPosX
```
number reaper.ImGui_GetCursorPosX(ImGui_Context ctx)
```

Cursor X position in window
## ImGui_GetCursorPosY
```
number reaper.ImGui_GetCursorPosY(ImGui_Context ctx)
```

Cursor Y position in window
## ImGui_GetCursorScreenPos
```
number x, number y = reaper.ImGui_GetCursorScreenPos(ImGui_Context ctx)
```

Cursor position in absolute screen coordinates (useful to work with the DrawList API).
## ImGui_GetCursorStartPos
```
number x, number y = reaper.ImGui_GetCursorStartPos(ImGui_Context ctx)
```

Initial cursor position in window coordinates.
## ImGui_GetDeltaTime
```
number reaper.ImGui_GetDeltaTime(ImGui_Context ctx)
```

Time elapsed since last frame, in seconds.
## ImGui_GetDragDropPayload
```
boolean retval, string type, string payload, boolean is_preview, boolean is_delivery = reaper.ImGui_GetDragDropPayload(ImGui_Context ctx)
```

Peek directly into the current payload from anywhere.
Returns false when drag and drop is finished or inactive.
## ImGui_GetDragDropPayloadFile
```
boolean retval, string filename = reaper.ImGui_GetDragDropPayloadFile(ImGui_Context ctx, integer index)
```

Get a filename from the list of dropped files.
Returns false if index is out of bounds.
## ImGui_GetFont
```
ImGui_Font reaper.ImGui_GetFont(ImGui_Context ctx)
```

Get the current font
## ImGui_GetFontSize
```
number reaper.ImGui_GetFontSize(ImGui_Context ctx)
```

Get current font size (= height in pixels) of current font with current scale
applied.
## ImGui_GetForegroundDrawList
```
ImGui_DrawList reaper.ImGui_GetForegroundDrawList(ImGui_Context ctx)
```

This draw list will be the last rendered one. Useful to quickly draw
shapes/text over dear imgui contents.
## ImGui_GetFrameCount
```
integer reaper.ImGui_GetFrameCount(ImGui_Context ctx)
```

Get global imgui frame count. incremented by 1 every frame.
## ImGui_GetFrameHeight
```
number reaper.ImGui_GetFrameHeight(ImGui_Context ctx)
```

GetFontSize + StyleVar_FramePadding.y * 2
## ImGui_GetFrameHeightWithSpacing
```
number reaper.ImGui_GetFrameHeightWithSpacing(ImGui_Context ctx)
```

GetFontSize + StyleVar_FramePadding.y * 2 + StyleVar_ItemSpacing.y
(distance in pixels between 2 consecutive lines of framed widgets).
## ImGui_GetFramerate
```
number reaper.ImGui_GetFramerate(ImGui_Context ctx)
```

Estimate of application framerate (rolling average over 60 frames, based on
GetDeltaTime), in frame per second. Solely for convenience.
## ImGui_GetInputQueueCharacter
```
boolean retval, integer unicode_char = reaper.ImGui_GetInputQueueCharacter(ImGui_Context ctx, integer idx)
```

Read from ImGui's character input queue.
Call with increasing idx until false is returned.
## ImGui_GetItemRectMax
```
number x, number y = reaper.ImGui_GetItemRectMax(ImGui_Context ctx)
```

Get lower-right bounding rectangle of the last item (screen space)
## ImGui_GetItemRectMin
```
number x, number y = reaper.ImGui_GetItemRectMin(ImGui_Context ctx)
```

Get upper-left bounding rectangle of the last item (screen space)
## ImGui_GetItemRectSize
```
number w, number h = reaper.ImGui_GetItemRectSize(ImGui_Context ctx)
```

Get size of last item
## ImGui_GetKeyDownDuration
```
number reaper.ImGui_GetKeyDownDuration(ImGui_Context ctx, integer key)
```

Duration the keyboard key has been down (0.0 == just pressed)
## ImGui_GetKeyMods
```
integer reaper.ImGui_GetKeyMods(ImGui_Context ctx)
```

Flags for the Ctrl/Shift/Alt/Super keys. Uses Mod_* values.
## ImGui_GetKeyPressedAmount
```
integer reaper.ImGui_GetKeyPressedAmount(ImGui_Context ctx, integer key, number repeat_delay, number rate)
```

Uses provided repeat rate/delay. Return a count, most often 0 or 1 but might
be >1 if ConfigVar_RepeatRate is small enough that GetDeltaTime > RepeatRate.
## ImGui_GetMainViewport
```
ImGui_Viewport reaper.ImGui_GetMainViewport(ImGui_Context ctx)
```

Currently represents REAPER's main window (arrange view).
WARNING: This may change or be removed in the future.
## ImGui_GetMouseClickedCount
```
integer reaper.ImGui_GetMouseClickedCount(ImGui_Context ctx, integer button)
```

Return the number of successive mouse-clicks at the time where a click happen (otherwise 0).
## ImGui_GetMouseClickedPos
```
number x, number y = reaper.ImGui_GetMouseClickedPos(ImGui_Context ctx, integer button)
```

No description available.
## ImGui_GetMouseCursor
```
integer reaper.ImGui_GetMouseCursor(ImGui_Context ctx)
```

Get desired mouse cursor shape, reset every frame. This is updated during the frame.
## ImGui_GetMouseDelta
```
number x, number y = reaper.ImGui_GetMouseDelta(ImGui_Context ctx)
```

Mouse delta. Note that this is zero if either current or previous position
are invalid (-FLT_MAX,-FLT_MAX), so a disappearing/reappearing mouse won't have
a huge delta.
## ImGui_GetMouseDownDuration
```
number reaper.ImGui_GetMouseDownDuration(ImGui_Context ctx, integer button)
```

Duration the mouse button has been down (0.0 == just clicked)
## ImGui_GetMouseDragDelta
```
number x, number y = reaper.ImGui_GetMouseDragDelta(ImGui_Context ctx, number x, number y, optional integer buttonIn, optional number lock_thresholdIn)
```

Return the delta from the initial clicking position while the mouse button is
pressed or was just released. This is locked and return 0.0 until the mouse
moves past a distance threshold at least once (uses ConfigVar_MouseDragThreshold
if lock_threshold < 0.0).
## ImGui_GetMousePos
```
number x, number y = reaper.ImGui_GetMousePos(ImGui_Context ctx)
```

No description available.
## ImGui_GetMousePosOnOpeningCurrentPopup
```
number x, number y = reaper.ImGui_GetMousePosOnOpeningCurrentPopup(ImGui_Context ctx)
```

Retrieve mouse position at the time of opening popup we have BeginPopup()
into (helper to avoid user backing that value themselves).
## ImGui_GetMouseWheel
```
number vertical, number horizontal = reaper.ImGui_GetMouseWheel(ImGui_Context ctx)
```

Vertical: 1 unit scrolls about 5 lines text. >0 scrolls Up, <0 scrolls Down.
Hold SHIFT to turn vertical scroll into horizontal scroll
## ImGui_GetScrollMaxX
```
number reaper.ImGui_GetScrollMaxX(ImGui_Context ctx)
```

Get maximum scrolling amount ~~ ContentSize.x - WindowSize.x - DecorationsSize.x
## ImGui_GetScrollMaxY
```
number reaper.ImGui_GetScrollMaxY(ImGui_Context ctx)
```

Get maximum scrolling amount ~~ ContentSize.y - WindowSize.y - DecorationsSize.y
## ImGui_GetScrollX
```
number reaper.ImGui_GetScrollX(ImGui_Context ctx)
```

Get scrolling amount [0 .. GetScrollMaxX()]
## ImGui_GetScrollY
```
number reaper.ImGui_GetScrollY(ImGui_Context ctx)
```

Get scrolling amount [0 .. GetScrollMaxY()]
## ImGui_GetStyleColor
```
integer reaper.ImGui_GetStyleColor(ImGui_Context ctx, integer idx)
```

Retrieve style color as stored in ImGuiStyle structure.
Use to feed back into PushStyleColor, Otherwise use GetColor to get style color
with style alpha baked in. See Col_* for available style colors.
## ImGui_GetStyleVar
```
number val1, number val2 = reaper.ImGui_GetStyleVar(ImGui_Context ctx, integer var_idx)
```

No description available.
## ImGui_GetTextLineHeight
```
number reaper.ImGui_GetTextLineHeight(ImGui_Context ctx)
```

Same as GetFontSize
## ImGui_GetTextLineHeightWithSpacing
```
number reaper.ImGui_GetTextLineHeightWithSpacing(ImGui_Context ctx)
```

GetFontSize + StyleVar_ItemSpacing.y
(distance in pixels between 2 consecutive lines of text).
## ImGui_GetTime
```
number reaper.ImGui_GetTime(ImGui_Context ctx)
```

Get global imgui time. Incremented every frame.
## ImGui_GetTreeNodeToLabelSpacing
```
number reaper.ImGui_GetTreeNodeToLabelSpacing(ImGui_Context ctx)
```

Horizontal distance preceding label when using TreeNode*() or Bullet()
== (GetFontSize + StyleVar_FramePadding.x*2) for a regular unframed TreeNode.
## ImGui_GetVersion
```
string imgui_version, integer imgui_version_num, string reaimgui_version = reaper.ImGui_GetVersion()
```

No description available.
## ImGui_GetWindowContentRegionMax
```
number x, number y = reaper.ImGui_GetWindowContentRegionMax(ImGui_Context ctx)
```

Content boundaries max (roughly (0,0)+Size-Scroll) where Size can be
overridden with SetNextWindowContentSize, in window coordinates.
## ImGui_GetWindowContentRegionMin
```
number x, number y = reaper.ImGui_GetWindowContentRegionMin(ImGui_Context ctx)
```

Content boundaries min (roughly (0,0)-Scroll), in window coordinates.
## ImGui_GetWindowDockID
```
integer reaper.ImGui_GetWindowDockID(ImGui_Context ctx)
```

No description available.
## ImGui_GetWindowDpiScale
```
number reaper.ImGui_GetWindowDpiScale(ImGui_Context ctx)
```

Get DPI scale currently associated to the current window's viewport
(1.0 = 96 DPI).
## ImGui_GetWindowDrawList
```
ImGui_DrawList reaper.ImGui_GetWindowDrawList(ImGui_Context ctx)
```

The draw list associated to the current window, to append your own drawing primitives
## ImGui_GetWindowHeight
```
number reaper.ImGui_GetWindowHeight(ImGui_Context ctx)
```

Get current window height (shortcut for (GetWindowSize().h).
## ImGui_GetWindowPos
```
number x, number y = reaper.ImGui_GetWindowPos(ImGui_Context ctx)
```

Get current window position in screen space (note: it is unlikely you need to
use this. Consider using current layout pos instead, GetCursorScreenPos()).
## ImGui_GetWindowSize
```
number w, number h = reaper.ImGui_GetWindowSize(ImGui_Context ctx)
```

Get current window size (note: it is unlikely you need to use this.
Consider using GetCursorScreenPos() and e.g. GetContentRegionAvail() instead)
## ImGui_GetWindowViewport
```
ImGui_Viewport reaper.ImGui_GetWindowViewport(ImGui_Context ctx)
```

Get viewport currently associated to the current window.
## ImGui_GetWindowWidth
```
number reaper.ImGui_GetWindowWidth(ImGui_Context ctx)
```

Get current window width (shortcut for (GetWindowSize().w).
## ImGui_HoveredFlags_AllowWhenBlockedByActiveItem
```
integer reaper.ImGui_HoveredFlags_AllowWhenBlockedByActiveItem()
```

Return true even if an active item is blocking access to this item/window. Useful for Drag and Drop patterns.
## ImGui_HoveredFlags_AllowWhenBlockedByPopup
```
integer reaper.ImGui_HoveredFlags_AllowWhenBlockedByPopup()
```

Return true even if a popup window is normally blocking access to this item/window.
## ImGui_HoveredFlags_AllowWhenDisabled
```
integer reaper.ImGui_HoveredFlags_AllowWhenDisabled()
```

Return true even if the item is disabled.
## ImGui_HoveredFlags_AllowWhenOverlapped
```
integer reaper.ImGui_HoveredFlags_AllowWhenOverlapped()
```

HoveredFlags_AllowWhenOverlappedByItem | HoveredFlags_AllowWhenOverlappedByWindow
## ImGui_HoveredFlags_AllowWhenOverlappedByItem
```
integer reaper.ImGui_HoveredFlags_AllowWhenOverlappedByItem()
```

Return true even if the item uses AllowOverlap mode and is overlapped by another hoverable item.
## ImGui_HoveredFlags_AllowWhenOverlappedByWindow
```
integer reaper.ImGui_HoveredFlags_AllowWhenOverlappedByWindow()
```

Return true even if the position is obstructed or overlapped by another window.
## ImGui_HoveredFlags_AnyWindow
```
integer reaper.ImGui_HoveredFlags_AnyWindow()
```

Return true if any window is hovered.
## ImGui_HoveredFlags_ChildWindows
```
integer reaper.ImGui_HoveredFlags_ChildWindows()
```

Return true if any children of the window is hovered.
## ImGui_HoveredFlags_DelayNone
```
integer reaper.ImGui_HoveredFlags_DelayNone()
```

Return true immediately (default). As this is the default you generally ignore this.
## ImGui_HoveredFlags_DelayNormal
```
integer reaper.ImGui_HoveredFlags_DelayNormal()
```

Return true after ConfigVar_HoverDelayNormal elapsed (~0.40 sec) (shared between items) + requires mouse to be stationary for ConfigVar_HoverStationaryDelay (once per item).
## ImGui_HoveredFlags_DelayShort
```
integer reaper.ImGui_HoveredFlags_DelayShort()
```

Return true after ConfigVar_HoverDelayShort elapsed (~0.15 sec) (shared between items) + requires mouse to be stationary for ConfigVar_HoverStationaryDelay (once per item).
## ImGui_HoveredFlags_DockHierarchy
```
integer reaper.ImGui_HoveredFlags_DockHierarchy()
```

Consider docking hierarchy (treat dockspace host as parent of docked window) (when used with _ChildWindows or _RootWindow).
## ImGui_HoveredFlags_ForTooltip
```
integer reaper.ImGui_HoveredFlags_ForTooltip()
```

Typically used with IsItemHovered() before SetTooltip(). This is a shortcut to pull flags from ConfigVar_HoverFlagsForTooltip* where you can reconfigure the desired behavior.
## ImGui_HoveredFlags_NoNavOverride
```
integer reaper.ImGui_HoveredFlags_NoNavOverride()
```

Disable using gamepad/keyboard navigation state when active, always query mouse.
## ImGui_HoveredFlags_NoPopupHierarchy
```
integer reaper.ImGui_HoveredFlags_NoPopupHierarchy()
```

Do not consider popup hierarchy (do not treat popup emitter as parent of popup) (when used with _ChildWindows or _RootWindow).
## ImGui_HoveredFlags_NoSharedDelay
```
integer reaper.ImGui_HoveredFlags_NoSharedDelay()
```

Disable shared delay system where moving from one item to the next keeps the previous timer for a short time (standard for tooltips with long delays
## ImGui_HoveredFlags_None
```
integer reaper.ImGui_HoveredFlags_None()
```

Return true if directly over the item/window, not obstructed by another window, not obstructed by an active popup or modal blocking inputs under them.
## ImGui_HoveredFlags_RectOnly
```
integer reaper.ImGui_HoveredFlags_RectOnly()
```

HoveredFlags_AllowWhenBlockedByPopup | HoveredFlags_AllowWhenBlockedByActiveItem | HoveredFlags_AllowWhenOverlapped
## ImGui_HoveredFlags_RootAndChildWindows
```
integer reaper.ImGui_HoveredFlags_RootAndChildWindows()
```

HoveredFlags_RootWindow | HoveredFlags_ChildWindows
## ImGui_HoveredFlags_RootWindow
```
integer reaper.ImGui_HoveredFlags_RootWindow()
```

Test from root window (top most parent of the current hierarchy).
## ImGui_HoveredFlags_Stationary
```
integer reaper.ImGui_HoveredFlags_Stationary()
```

Require mouse to be stationary for ConfigVar_HoverStationaryDelay (~0.15 sec) _at least one time_. After this, can move on same item/window. Using the stationary test tends to reduces the need for a long delay.
## ImGui_Image
```
reaper.ImGui_Image(ImGui_Context ctx, ImGui_Image image, number image_size_w, number image_size_h, optional number uv0_xIn, optional number uv0_yIn, optional number uv1_xIn, optional number uv1_yIn, optional integer tint_col_rgbaIn, optional integer border_col_rgbaIn)
```

Adds 2.0 to the provided size if a border is visible.
## ImGui_ImageButton
```
boolean reaper.ImGui_ImageButton(ImGui_Context ctx, string str_id, ImGui_Image image, number image_size_w, number image_size_h, optional number uv0_xIn, optional number uv0_yIn, optional number uv1_xIn, optional number uv1_yIn, optional integer bg_col_rgbaIn, optional integer tint_col_rgbaIn)
```

Adds StyleVar_FramePadding*2.0 to provided size.
## ImGui_ImageSet_Add
```
reaper.ImGui_ImageSet_Add(ImGui_ImageSet set, number scale, ImGui_Image image)
```

'img' cannot be another ImageSet.
## ImGui_Image_GetSize
```
number w, number h = reaper.ImGui_Image_GetSize(ImGui_Image image)
```

No description available.
## ImGui_Indent
```
reaper.ImGui_Indent(ImGui_Context ctx, optional number indent_wIn)
```

Move content position toward the right, by 'indent_w', or
StyleVar_IndentSpacing if 'indent_w' <= 0. See Unindent.
## ImGui_InputDouble
```
boolean retval, number v = reaper.ImGui_InputDouble(ImGui_Context ctx, string label, number v, optional number stepIn, optional number step_fastIn, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_InputDouble2
```
boolean retval, number v1, number v2 = reaper.ImGui_InputDouble2(ImGui_Context ctx, string label, number v1, number v2, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_InputDouble3
```
boolean retval, number v1, number v2, number v3 = reaper.ImGui_InputDouble3(ImGui_Context ctx, string label, number v1, number v2, number v3, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_InputDouble4
```
boolean retval, number v1, number v2, number v3, number v4 = reaper.ImGui_InputDouble4(ImGui_Context ctx, string label, number v1, number v2, number v3, number v4, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_InputDoubleN
```
boolean reaper.ImGui_InputDoubleN(ImGui_Context ctx, string label, reaper_array values, optional number stepIn, optional number step_fastIn, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_InputFlags_None
```
integer reaper.ImGui_InputFlags_None()
```

No description available.
## ImGui_InputFlags_Repeat
```
integer reaper.ImGui_InputFlags_Repeat()
```

Enable repeat. Return true on successive repeats.
## ImGui_InputFlags_RouteActive
```
integer reaper.ImGui_InputFlags_RouteActive()
```

Route to active item only.
## ImGui_InputFlags_RouteAlways
```
integer reaper.ImGui_InputFlags_RouteAlways()
```

Do not register route, poll keys directly.
## ImGui_InputFlags_RouteFocused
```
integer reaper.ImGui_InputFlags_RouteFocused()
```

Route to windows in the focus stack. Deep-most focused window takes inputs. Active item takes inputs over deep-most focused window.
## ImGui_InputFlags_RouteFromRootWindow
```
integer reaper.ImGui_InputFlags_RouteFromRootWindow()
```

Option: route evaluated from the point of view of root window rather than current window.
## ImGui_InputFlags_RouteGlobal
```
integer reaper.ImGui_InputFlags_RouteGlobal()
```

Global route (unless a focused window or active item registered the route).
## ImGui_InputFlags_RouteOverActive
```
integer reaper.ImGui_InputFlags_RouteOverActive()
```

Global route: higher priority than active item. Unlikely you need to use that: will interfere with every active items, e.g. Ctrl+A registered by InputText will be overridden by this. May not be fully honored as user/internal code is likely to always assume they can access keys when active.
## ImGui_InputFlags_RouteOverFocused
```
integer reaper.ImGui_InputFlags_RouteOverFocused()
```

Global route: higher priority than focused route (unless active item in focused route).
## ImGui_InputFlags_RouteUnlessBgFocused
```
integer reaper.ImGui_InputFlags_RouteUnlessBgFocused()
```

Option: global route: will not be applied if underlying background/void is focused (== no Dear ImGui windows are focused). Useful for overlay applications.
## ImGui_InputFlags_Tooltip
```
integer reaper.ImGui_InputFlags_Tooltip()
```

Automatically display a tooltip when hovering item
## ImGui_InputInt
```
boolean retval, integer v = reaper.ImGui_InputInt(ImGui_Context ctx, string label, integer v, optional integer stepIn, optional integer step_fastIn, optional integer flagsIn)
```

No description available.
## ImGui_InputInt2
```
boolean retval, integer v1, integer v2 = reaper.ImGui_InputInt2(ImGui_Context ctx, string label, integer v1, integer v2, optional integer flagsIn)
```

No description available.
## ImGui_InputInt3
```
boolean retval, integer v1, integer v2, integer v3 = reaper.ImGui_InputInt3(ImGui_Context ctx, string label, integer v1, integer v2, integer v3, optional integer flagsIn)
```

No description available.
## ImGui_InputInt4
```
boolean retval, integer v1, integer v2, integer v3, integer v4 = reaper.ImGui_InputInt4(ImGui_Context ctx, string label, integer v1, integer v2, integer v3, integer v4, optional integer flagsIn)
```

No description available.
## ImGui_InputText
```
boolean retval, string buf = reaper.ImGui_InputText(ImGui_Context ctx, string label, string buf, optional integer flagsIn, ImGui_Function callbackIn)
```

No description available.
## ImGui_InputTextFlags_AllowTabInput
```
integer reaper.ImGui_InputTextFlags_AllowTabInput()
```

Pressing TAB input a '\t' character into the text field.
## ImGui_InputTextFlags_AlwaysOverwrite
```
integer reaper.ImGui_InputTextFlags_AlwaysOverwrite()
```

Overwrite mode.
## ImGui_InputTextFlags_AutoSelectAll
```
integer reaper.ImGui_InputTextFlags_AutoSelectAll()
```

Select entire text when first taking mouse focus.
## ImGui_InputTextFlags_CallbackAlways
```
integer reaper.ImGui_InputTextFlags_CallbackAlways()
```

Callback on each iteration. User code may query cursor position, modify text buffer.
## ImGui_InputTextFlags_CallbackCharFilter
```
integer reaper.ImGui_InputTextFlags_CallbackCharFilter()
```

Callback on character inputs to replace or discard them. Modify 'EventChar' to replace or 'EventChar = 0' to discard.
## ImGui_InputTextFlags_CallbackCompletion
```
integer reaper.ImGui_InputTextFlags_CallbackCompletion()
```

Callback on pressing TAB (for completion handling).
## ImGui_InputTextFlags_CallbackEdit
```
integer reaper.ImGui_InputTextFlags_CallbackEdit()
```

Callback on any edit (note that InputText() already returns true on edit, the callback is useful mainly to manipulate the underlying buffer while focus is active).
## ImGui_InputTextFlags_CallbackHistory
```
integer reaper.ImGui_InputTextFlags_CallbackHistory()
```

Callback on pressing Up/Down arrows (for history handling).
## ImGui_InputTextFlags_CharsDecimal
```
integer reaper.ImGui_InputTextFlags_CharsDecimal()
```

Allow 0123456789.+-*/.
## ImGui_InputTextFlags_CharsHexadecimal
```
integer reaper.ImGui_InputTextFlags_CharsHexadecimal()
```

Allow 0123456789ABCDEFabcdef.
## ImGui_InputTextFlags_CharsNoBlank
```
integer reaper.ImGui_InputTextFlags_CharsNoBlank()
```

Filter out spaces, tabs.
## ImGui_InputTextFlags_CharsScientific
```
integer reaper.ImGui_InputTextFlags_CharsScientific()
```

Allow 0123456789.+-*/eE (Scientific notation input).
## ImGui_InputTextFlags_CharsUppercase
```
integer reaper.ImGui_InputTextFlags_CharsUppercase()
```

Turn a..z into A..Z.
## ImGui_InputTextFlags_CtrlEnterForNewLine
```
integer reaper.ImGui_InputTextFlags_CtrlEnterForNewLine()
```

In multi-line mode, unfocus with Enter, add new line with Ctrl+Enter (default is opposite: unfocus with Ctrl+Enter, add line with Enter).
## ImGui_InputTextFlags_DisplayEmptyRefVal
```
integer reaper.ImGui_InputTextFlags_DisplayEmptyRefVal()
```

InputDouble(), InputInt() etc. only: when value is zero, do not display it. Generally used with InputTextFlags_ParseEmptyRefVal.
## ImGui_InputTextFlags_EnterReturnsTrue
```
integer reaper.ImGui_InputTextFlags_EnterReturnsTrue()
```

Return 'true' when Enter is pressed (as opposed to every time the value was modified). Consider looking at the IsItemDeactivatedAfterEdit function.
## ImGui_InputTextFlags_EscapeClearsAll
```
integer reaper.ImGui_InputTextFlags_EscapeClearsAll()
```

Escape key clears content if not empty, and deactivate otherwise (constrast to default behavior of Escape to revert).
## ImGui_InputTextFlags_NoHorizontalScroll
```
integer reaper.ImGui_InputTextFlags_NoHorizontalScroll()
```

Disable following the cursor horizontally.
## ImGui_InputTextFlags_NoUndoRedo
```
integer reaper.ImGui_InputTextFlags_NoUndoRedo()
```

Disable undo/redo. Note that input text owns the text data while active.
## ImGui_InputTextFlags_None
```
integer reaper.ImGui_InputTextFlags_None()
```

No description available.
## ImGui_InputTextFlags_ParseEmptyRefVal
```
integer reaper.ImGui_InputTextFlags_ParseEmptyRefVal()
```

InputDouble(), InputInt() etc. only: parse empty string as zero value.
## ImGui_InputTextFlags_Password
```
integer reaper.ImGui_InputTextFlags_Password()
```

Password mode, display all characters as '*'.
## ImGui_InputTextFlags_ReadOnly
```
integer reaper.ImGui_InputTextFlags_ReadOnly()
```

Read-only mode.
## ImGui_InputTextMultiline
```
boolean retval, string buf = reaper.ImGui_InputTextMultiline(ImGui_Context ctx, string label, string buf, optional number size_wIn, optional number size_hIn, optional integer flagsIn, ImGui_Function callbackIn)
```

No description available.
## ImGui_InputTextWithHint
```
boolean retval, string buf = reaper.ImGui_InputTextWithHint(ImGui_Context ctx, string label, string hint, string buf, optional integer flagsIn, ImGui_Function callbackIn)
```

No description available.
## ImGui_InvisibleButton
```
boolean reaper.ImGui_InvisibleButton(ImGui_Context ctx, string str_id, number size_w, number size_h, optional integer flagsIn)
```

Flexible button behavior without the visuals, frequently useful to build
custom behaviors using the public api (along with IsItemActive, IsItemHovered, etc.).
## ImGui_IsAnyItemActive
```
boolean reaper.ImGui_IsAnyItemActive(ImGui_Context ctx)
```

No description available.
## ImGui_IsAnyItemFocused
```
boolean reaper.ImGui_IsAnyItemFocused(ImGui_Context ctx)
```

No description available.
## ImGui_IsAnyItemHovered
```
boolean reaper.ImGui_IsAnyItemHovered(ImGui_Context ctx)
```

No description available.
## ImGui_IsAnyMouseDown
```
boolean reaper.ImGui_IsAnyMouseDown(ImGui_Context ctx)
```

Is any mouse button held?
## ImGui_IsItemActivated
```
boolean reaper.ImGui_IsItemActivated(ImGui_Context ctx)
```

Was the last item just made active (item was previously inactive).
## ImGui_IsItemActive
```
boolean reaper.ImGui_IsItemActive(ImGui_Context ctx)
```

Is the last item active? (e.g. button being held, text field being edited.
This will continuously return true while holding mouse button on an item.
Items that don't interact will always return false.
## ImGui_IsItemClicked
```
boolean reaper.ImGui_IsItemClicked(ImGui_Context ctx, optional integer mouse_buttonIn)
```

Is the last item clicked? (e.g. button/node just clicked on)
== IsMouseClicked(mouse_button) && IsItemHovered().
## ImGui_IsItemDeactivated
```
boolean reaper.ImGui_IsItemDeactivated(ImGui_Context ctx)
```

Was the last item just made inactive (item was previously active).
Useful for Undo/Redo patterns with widgets that require continuous editing.
## ImGui_IsItemDeactivatedAfterEdit
```
boolean reaper.ImGui_IsItemDeactivatedAfterEdit(ImGui_Context ctx)
```

Was the last item just made inactive and made a value change when it was
active? (e.g. Slider/Drag moved).
## ImGui_IsItemEdited
```
boolean reaper.ImGui_IsItemEdited(ImGui_Context ctx)
```

Did the last item modify its underlying value this frame? or was pressed?
This is generally the same as the "bool" return value of many widgets.
## ImGui_IsItemFocused
```
boolean reaper.ImGui_IsItemFocused(ImGui_Context ctx)
```

Is the last item focused for keyboard/gamepad navigation?
## ImGui_IsItemHovered
```
boolean reaper.ImGui_IsItemHovered(ImGui_Context ctx, optional integer flagsIn)
```

Is the last item hovered? (and usable, aka not blocked by a popup, etc.).
See HoveredFlags_* for more options.
## ImGui_IsItemToggledOpen
```
boolean reaper.ImGui_IsItemToggledOpen(ImGui_Context ctx)
```

Was the last item open state toggled? Set by TreeNode.
## ImGui_IsItemVisible
```
boolean reaper.ImGui_IsItemVisible(ImGui_Context ctx)
```

Is the last item visible? (items may be out of sight because of clipping/scrolling)
## ImGui_IsKeyChordPressed
```
boolean reaper.ImGui_IsKeyChordPressed(ImGui_Context ctx, integer key_chord)
```

Was key chord (mods + key) pressed? You can pass e.g. `Mod_Ctrl | Key_S`
as a key chord. This doesn't do any routing or focus check, consider using the
Shortcut function instead.
## ImGui_IsKeyDown
```
boolean reaper.ImGui_IsKeyDown(ImGui_Context ctx, integer key)
```

Is key being held.
## ImGui_IsKeyPressed
```
boolean reaper.ImGui_IsKeyPressed(ImGui_Context ctx, integer key, optional boolean repeatIn)
```

Was key pressed (went from !Down to Down)?
If repeat=true, uses ConfigVar_KeyRepeatDelay / ConfigVar_KeyRepeatRate.
## ImGui_IsKeyReleased
```
boolean reaper.ImGui_IsKeyReleased(ImGui_Context ctx, integer key)
```

Was key released (went from Down to !Down)?
## ImGui_IsMouseClicked
```
boolean reaper.ImGui_IsMouseClicked(ImGui_Context ctx, integer button, optional boolean repeatIn)
```

Did mouse button clicked? (went from !Down to Down).
Same as GetMouseClickedCount() == 1.
## ImGui_IsMouseDoubleClicked
```
boolean reaper.ImGui_IsMouseDoubleClicked(ImGui_Context ctx, integer button)
```

Did mouse button double-clicked? Same as GetMouseClickedCount() == 2.
(Note that a double-click will also report IsMouseClicked() == true)
## ImGui_IsMouseDown
```
boolean reaper.ImGui_IsMouseDown(ImGui_Context ctx, integer button)
```

Is mouse button held?
## ImGui_IsMouseDragging
```
boolean reaper.ImGui_IsMouseDragging(ImGui_Context ctx, integer button, optional number lock_thresholdIn)
```

Is mouse dragging? (uses ConfigVar_MouseDragThreshold if lock_threshold < 0.0)
## ImGui_IsMouseHoveringRect
```
boolean reaper.ImGui_IsMouseHoveringRect(ImGui_Context ctx, number r_min_x, number r_min_y, number r_max_x, number r_max_y, optional boolean clipIn)
```

Is mouse hovering given bounding rect (in screen space).
Clipped by current clipping settings, but disregarding of other consideration
of focus/window ordering/popup-block.
## ImGui_IsMousePosValid
```
boolean reaper.ImGui_IsMousePosValid(ImGui_Context ctx, optional number mouse_pos_xIn, optional number mouse_pos_yIn)
```

No description available.
## ImGui_IsMouseReleased
```
boolean reaper.ImGui_IsMouseReleased(ImGui_Context ctx, integer button)
```

Did mouse button released? (went from Down to !Down)
## ImGui_IsPopupOpen
```
boolean reaper.ImGui_IsPopupOpen(ImGui_Context ctx, string str_id, optional integer flagsIn)
```

Return true if the popup is open at the current BeginPopup level of the
popup stack.
## ImGui_IsRectVisible
```
boolean reaper.ImGui_IsRectVisible(ImGui_Context ctx, number size_w, number size_h)
```

Test if rectangle (of given size, starting from cursor position) is
visible / not clipped.
## ImGui_IsRectVisibleEx
```
boolean reaper.ImGui_IsRectVisibleEx(ImGui_Context ctx, number rect_min_x, number rect_min_y, number rect_max_x, number rect_max_y)
```

Test if rectangle (in screen space) is visible / not clipped. to perform
coarse clipping on user's side.
## ImGui_IsWindowAppearing
```
boolean reaper.ImGui_IsWindowAppearing(ImGui_Context ctx)
```

Use after Begin/BeginPopup/BeginPopupModal to tell if a window just opened.
## ImGui_IsWindowDocked
```
boolean reaper.ImGui_IsWindowDocked(ImGui_Context ctx)
```

Is current window docked into another window or a REAPER docker?
## ImGui_IsWindowFocused
```
boolean reaper.ImGui_IsWindowFocused(ImGui_Context ctx, optional integer flagsIn)
```

Is current window focused? or its root/child, depending on flags.
See flags for options.
## ImGui_IsWindowHovered
```
boolean reaper.ImGui_IsWindowHovered(ImGui_Context ctx, optional integer flagsIn)
```

Is current window hovered and hoverable (e.g. not blocked by a popup/modal)?
See HoveredFlags_* for options.
## ImGui_Key_0
```
integer reaper.ImGui_Key_0()
```

No description available.
## ImGui_Key_1
```
integer reaper.ImGui_Key_1()
```

No description available.
## ImGui_Key_2
```
integer reaper.ImGui_Key_2()
```

No description available.
## ImGui_Key_3
```
integer reaper.ImGui_Key_3()
```

No description available.
## ImGui_Key_4
```
integer reaper.ImGui_Key_4()
```

No description available.
## ImGui_Key_5
```
integer reaper.ImGui_Key_5()
```

No description available.
## ImGui_Key_6
```
integer reaper.ImGui_Key_6()
```

No description available.
## ImGui_Key_7
```
integer reaper.ImGui_Key_7()
```

No description available.
## ImGui_Key_8
```
integer reaper.ImGui_Key_8()
```

No description available.
## ImGui_Key_9
```
integer reaper.ImGui_Key_9()
```

No description available.
## ImGui_Key_A
```
integer reaper.ImGui_Key_A()
```

No description available.
## ImGui_Key_Apostrophe
```
integer reaper.ImGui_Key_Apostrophe()
```

'
## ImGui_Key_AppBack
```
integer reaper.ImGui_Key_AppBack()
```

Available on some keyboard/mouses. Often referred as "Browser Back".
## ImGui_Key_AppForward
```
integer reaper.ImGui_Key_AppForward()
```

No description available.
## ImGui_Key_B
```
integer reaper.ImGui_Key_B()
```

No description available.
## ImGui_Key_Backslash
```
integer reaper.ImGui_Key_Backslash()
```

\
## ImGui_Key_Backspace
```
integer reaper.ImGui_Key_Backspace()
```

No description available.
## ImGui_Key_C
```
integer reaper.ImGui_Key_C()
```

No description available.
## ImGui_Key_CapsLock
```
integer reaper.ImGui_Key_CapsLock()
```

No description available.
## ImGui_Key_Comma
```
integer reaper.ImGui_Key_Comma()
```

,
## ImGui_Key_D
```
integer reaper.ImGui_Key_D()
```

No description available.
## ImGui_Key_Delete
```
integer reaper.ImGui_Key_Delete()
```

No description available.
## ImGui_Key_DownArrow
```
integer reaper.ImGui_Key_DownArrow()
```

No description available.
## ImGui_Key_E
```
integer reaper.ImGui_Key_E()
```

No description available.
## ImGui_Key_End
```
integer reaper.ImGui_Key_End()
```

No description available.
## ImGui_Key_Enter
```
integer reaper.ImGui_Key_Enter()
```

No description available.
## ImGui_Key_Equal
```
integer reaper.ImGui_Key_Equal()
```

=
## ImGui_Key_Escape
```
integer reaper.ImGui_Key_Escape()
```

No description available.
## ImGui_Key_F
```
integer reaper.ImGui_Key_F()
```

No description available.
## ImGui_Key_F1
```
integer reaper.ImGui_Key_F1()
```

No description available.
## ImGui_Key_F10
```
integer reaper.ImGui_Key_F10()
```

No description available.
## ImGui_Key_F11
```
integer reaper.ImGui_Key_F11()
```

No description available.
## ImGui_Key_F12
```
integer reaper.ImGui_Key_F12()
```

No description available.
## ImGui_Key_F13
```
integer reaper.ImGui_Key_F13()
```

No description available.
## ImGui_Key_F14
```
integer reaper.ImGui_Key_F14()
```

No description available.
## ImGui_Key_F15
```
integer reaper.ImGui_Key_F15()
```

No description available.
## ImGui_Key_F16
```
integer reaper.ImGui_Key_F16()
```

No description available.
## ImGui_Key_F17
```
integer reaper.ImGui_Key_F17()
```

No description available.
## ImGui_Key_F18
```
integer reaper.ImGui_Key_F18()
```

No description available.
## ImGui_Key_F19
```
integer reaper.ImGui_Key_F19()
```

No description available.
## ImGui_Key_F2
```
integer reaper.ImGui_Key_F2()
```

No description available.
## ImGui_Key_F20
```
integer reaper.ImGui_Key_F20()
```

No description available.
## ImGui_Key_F21
```
integer reaper.ImGui_Key_F21()
```

No description available.
## ImGui_Key_F22
```
integer reaper.ImGui_Key_F22()
```

No description available.
## ImGui_Key_F23
```
integer reaper.ImGui_Key_F23()
```

No description available.
## ImGui_Key_F24
```
integer reaper.ImGui_Key_F24()
```

No description available.
## ImGui_Key_F3
```
integer reaper.ImGui_Key_F3()
```

No description available.
## ImGui_Key_F4
```
integer reaper.ImGui_Key_F4()
```

No description available.
## ImGui_Key_F5
```
integer reaper.ImGui_Key_F5()
```

No description available.
## ImGui_Key_F6
```
integer reaper.ImGui_Key_F6()
```

No description available.
## ImGui_Key_F7
```
integer reaper.ImGui_Key_F7()
```

No description available.
## ImGui_Key_F8
```
integer reaper.ImGui_Key_F8()
```

No description available.
## ImGui_Key_F9
```
integer reaper.ImGui_Key_F9()
```

No description available.
## ImGui_Key_G
```
integer reaper.ImGui_Key_G()
```

No description available.
## ImGui_Key_GraveAccent
```
integer reaper.ImGui_Key_GraveAccent()
```

`
## ImGui_Key_H
```
integer reaper.ImGui_Key_H()
```

No description available.
## ImGui_Key_Home
```
integer reaper.ImGui_Key_Home()
```

No description available.
## ImGui_Key_I
```
integer reaper.ImGui_Key_I()
```

No description available.
## ImGui_Key_Insert
```
integer reaper.ImGui_Key_Insert()
```

No description available.
## ImGui_Key_J
```
integer reaper.ImGui_Key_J()
```

No description available.
## ImGui_Key_K
```
integer reaper.ImGui_Key_K()
```

No description available.
## ImGui_Key_Keypad0
```
integer reaper.ImGui_Key_Keypad0()
```

No description available.
## ImGui_Key_Keypad1
```
integer reaper.ImGui_Key_Keypad1()
```

No description available.
## ImGui_Key_Keypad2
```
integer reaper.ImGui_Key_Keypad2()
```

No description available.
## ImGui_Key_Keypad3
```
integer reaper.ImGui_Key_Keypad3()
```

No description available.
## ImGui_Key_Keypad4
```
integer reaper.ImGui_Key_Keypad4()
```

No description available.
## ImGui_Key_Keypad5
```
integer reaper.ImGui_Key_Keypad5()
```

No description available.
## ImGui_Key_Keypad6
```
integer reaper.ImGui_Key_Keypad6()
```

No description available.
## ImGui_Key_Keypad7
```
integer reaper.ImGui_Key_Keypad7()
```

No description available.
## ImGui_Key_Keypad8
```
integer reaper.ImGui_Key_Keypad8()
```

No description available.
## ImGui_Key_Keypad9
```
integer reaper.ImGui_Key_Keypad9()
```

No description available.
## ImGui_Key_KeypadAdd
```
integer reaper.ImGui_Key_KeypadAdd()
```

No description available.
## ImGui_Key_KeypadDecimal
```
integer reaper.ImGui_Key_KeypadDecimal()
```

No description available.
## ImGui_Key_KeypadDivide
```
integer reaper.ImGui_Key_KeypadDivide()
```

No description available.
## ImGui_Key_KeypadEnter
```
integer reaper.ImGui_Key_KeypadEnter()
```

No description available.
## ImGui_Key_KeypadEqual
```
integer reaper.ImGui_Key_KeypadEqual()
```

No description available.
## ImGui_Key_KeypadMultiply
```
integer reaper.ImGui_Key_KeypadMultiply()
```

No description available.
## ImGui_Key_KeypadSubtract
```
integer reaper.ImGui_Key_KeypadSubtract()
```

No description available.
## ImGui_Key_L
```
integer reaper.ImGui_Key_L()
```

No description available.
## ImGui_Key_LeftAlt
```
integer reaper.ImGui_Key_LeftAlt()
```

No description available.
## ImGui_Key_LeftArrow
```
integer reaper.ImGui_Key_LeftArrow()
```

No description available.
## ImGui_Key_LeftBracket
```
integer reaper.ImGui_Key_LeftBracket()
```

[
## ImGui_Key_LeftCtrl
```
integer reaper.ImGui_Key_LeftCtrl()
```

No description available.
## ImGui_Key_LeftShift
```
integer reaper.ImGui_Key_LeftShift()
```

No description available.
## ImGui_Key_LeftSuper
```
integer reaper.ImGui_Key_LeftSuper()
```

No description available.
## ImGui_Key_M
```
integer reaper.ImGui_Key_M()
```

No description available.
## ImGui_Key_Menu
```
integer reaper.ImGui_Key_Menu()
```

No description available.
## ImGui_Key_Minus
```
integer reaper.ImGui_Key_Minus()
```

-
## ImGui_Key_MouseLeft
```
integer reaper.ImGui_Key_MouseLeft()
```

No description available.
## ImGui_Key_MouseMiddle
```
integer reaper.ImGui_Key_MouseMiddle()
```

No description available.
## ImGui_Key_MouseRight
```
integer reaper.ImGui_Key_MouseRight()
```

No description available.
## ImGui_Key_MouseWheelX
```
integer reaper.ImGui_Key_MouseWheelX()
```

No description available.
## ImGui_Key_MouseWheelY
```
integer reaper.ImGui_Key_MouseWheelY()
```

No description available.
## ImGui_Key_MouseX1
```
integer reaper.ImGui_Key_MouseX1()
```

No description available.
## ImGui_Key_MouseX2
```
integer reaper.ImGui_Key_MouseX2()
```

No description available.
## ImGui_Key_N
```
integer reaper.ImGui_Key_N()
```

No description available.
## ImGui_Key_NumLock
```
integer reaper.ImGui_Key_NumLock()
```

No description available.
## ImGui_Key_O
```
integer reaper.ImGui_Key_O()
```

No description available.
## ImGui_Key_P
```
integer reaper.ImGui_Key_P()
```

No description available.
## ImGui_Key_PageDown
```
integer reaper.ImGui_Key_PageDown()
```

No description available.
## ImGui_Key_PageUp
```
integer reaper.ImGui_Key_PageUp()
```

No description available.
## ImGui_Key_Pause
```
integer reaper.ImGui_Key_Pause()
```

No description available.
## ImGui_Key_Period
```
integer reaper.ImGui_Key_Period()
```

.
## ImGui_Key_PrintScreen
```
integer reaper.ImGui_Key_PrintScreen()
```

No description available.
## ImGui_Key_Q
```
integer reaper.ImGui_Key_Q()
```

No description available.
## ImGui_Key_R
```
integer reaper.ImGui_Key_R()
```

No description available.
## ImGui_Key_RightAlt
```
integer reaper.ImGui_Key_RightAlt()
```

No description available.
## ImGui_Key_RightArrow
```
integer reaper.ImGui_Key_RightArrow()
```

No description available.
## ImGui_Key_RightBracket
```
integer reaper.ImGui_Key_RightBracket()
```

]
## ImGui_Key_RightCtrl
```
integer reaper.ImGui_Key_RightCtrl()
```

No description available.
## ImGui_Key_RightShift
```
integer reaper.ImGui_Key_RightShift()
```

No description available.
## ImGui_Key_RightSuper
```
integer reaper.ImGui_Key_RightSuper()
```

No description available.
## ImGui_Key_S
```
integer reaper.ImGui_Key_S()
```

No description available.
## ImGui_Key_ScrollLock
```
integer reaper.ImGui_Key_ScrollLock()
```

No description available.
## ImGui_Key_Semicolon
```
integer reaper.ImGui_Key_Semicolon()
```

;
## ImGui_Key_Slash
```
integer reaper.ImGui_Key_Slash()
```

/
## ImGui_Key_Space
```
integer reaper.ImGui_Key_Space()
```

No description available.
## ImGui_Key_T
```
integer reaper.ImGui_Key_T()
```

No description available.
## ImGui_Key_Tab
```
integer reaper.ImGui_Key_Tab()
```

No description available.
## ImGui_Key_U
```
integer reaper.ImGui_Key_U()
```

No description available.
## ImGui_Key_UpArrow
```
integer reaper.ImGui_Key_UpArrow()
```

No description available.
## ImGui_Key_V
```
integer reaper.ImGui_Key_V()
```

No description available.
## ImGui_Key_W
```
integer reaper.ImGui_Key_W()
```

No description available.
## ImGui_Key_X
```
integer reaper.ImGui_Key_X()
```

No description available.
## ImGui_Key_Y
```
integer reaper.ImGui_Key_Y()
```

No description available.
## ImGui_Key_Z
```
integer reaper.ImGui_Key_Z()
```

No description available.
## ImGui_LabelText
```
reaper.ImGui_LabelText(ImGui_Context ctx, string label, string text)
```

Display text+label aligned the same way as value+label widgets
## ImGui_ListBox
```
boolean retval, integer current_item = reaper.ImGui_ListBox(ImGui_Context ctx, string label, integer current_item, string items, optional integer height_in_itemsIn)
```

This is an helper over BeginListBox/EndListBox for convenience purpose.
## ImGui_ListClipper_Begin
```
reaper.ImGui_ListClipper_Begin(ImGui_ListClipper clipper, integer items_count, optional number items_heightIn)
```

- items_count: Use INT_MAX if you don't know how many items you have
(in which case the cursor won't be advanced in the final step)
- items_height: Use -1.0 to be calculated automatically on first step. Otherwise pass in the distance between your items, typically GetTextLineHeightWithSpacing or GetFrameHeightWithSpacing.
## ImGui_ListClipper_End
```
reaper.ImGui_ListClipper_End(ImGui_ListClipper clipper)
```

Automatically called on the last call of ListClipper_Step that returns false.
## ImGui_ListClipper_GetDisplayRange
```
integer display_start, integer display_end = reaper.ImGui_ListClipper_GetDisplayRange(ImGui_ListClipper clipper)
```

No description available.
## ImGui_ListClipper_IncludeItemByIndex
```
reaper.ImGui_ListClipper_IncludeItemByIndex(ImGui_ListClipper clipper, integer item_index)
```

Call ListClipper_IncludeItemByIndex or ListClipper_IncludeItemsByIndex before
the first call to ListClipper_Step if you need a range of items to be displayed
regardless of visibility.
## ImGui_ListClipper_IncludeItemsByIndex
```
reaper.ImGui_ListClipper_IncludeItemsByIndex(ImGui_ListClipper clipper, integer item_begin, integer item_end)
```

See ListClipper_IncludeItemByIndex.
## ImGui_ListClipper_Step
```
boolean reaper.ImGui_ListClipper_Step(ImGui_ListClipper clipper)
```

Call until it returns false. The display_start/display_end fields from
ListClipper_GetDisplayRange will be set and you can process/draw those items.
## ImGui_LogFinish
```
reaper.ImGui_LogFinish(ImGui_Context ctx)
```

Stop logging (close file, etc.)
## ImGui_LogText
```
reaper.ImGui_LogText(ImGui_Context ctx, string text)
```

Pass text data straight to log (without being displayed)
## ImGui_LogToClipboard
```
reaper.ImGui_LogToClipboard(ImGui_Context ctx, optional integer auto_open_depthIn)
```

Start logging all text output from the interface to the OS clipboard.
See also SetClipboardText.
## ImGui_LogToFile
```
reaper.ImGui_LogToFile(ImGui_Context ctx, optional integer auto_open_depthIn, optional string filenameIn)
```

Start logging all text output from the interface to a file.
The data is saved to $resource_path/imgui_log.txt if filename is nil.
## ImGui_LogToTTY
```
reaper.ImGui_LogToTTY(ImGui_Context ctx, optional integer auto_open_depthIn)
```

Start logging all text output from the interface to the TTY (stdout).
## ImGui_MenuItem
```
boolean retval, optional boolean p_selected = reaper.ImGui_MenuItem(ImGui_Context ctx, string label, optional string shortcutIn, optional boolean p_selected, optional boolean enabledIn)
```

Return true when activated. Shortcuts are displayed for convenience but not
processed by ImGui at the moment. Toggle state is written to 'selected' when
provided.
## ImGui_Mod_Alt
```
integer reaper.ImGui_Mod_Alt()
```

No description available.
## ImGui_Mod_Ctrl
```
integer reaper.ImGui_Mod_Ctrl()
```

Cmd when ConfigVar_MacOSXBehaviors is enabled.
## ImGui_Mod_None
```
integer reaper.ImGui_Mod_None()
```

No description available.
## ImGui_Mod_Shift
```
integer reaper.ImGui_Mod_Shift()
```

No description available.
## ImGui_Mod_Super
```
integer reaper.ImGui_Mod_Super()
```

Ctrl when ConfigVar_MacOSXBehaviors is enabled.
## ImGui_MouseButton_Left
```
integer reaper.ImGui_MouseButton_Left()
```

No description available.
## ImGui_MouseButton_Middle
```
integer reaper.ImGui_MouseButton_Middle()
```

No description available.
## ImGui_MouseButton_Right
```
integer reaper.ImGui_MouseButton_Right()
```

No description available.
## ImGui_MouseCursor_Arrow
```
integer reaper.ImGui_MouseCursor_Arrow()
```

No description available.
## ImGui_MouseCursor_Hand
```
integer reaper.ImGui_MouseCursor_Hand()
```

(Unused by Dear ImGui functions. Use for e.g. hyperlinks)
## ImGui_MouseCursor_None
```
integer reaper.ImGui_MouseCursor_None()
```

No description available.
## ImGui_MouseCursor_NotAllowed
```
integer reaper.ImGui_MouseCursor_NotAllowed()
```

When hovering something with disallowed interaction. Usually a crossed circle.
## ImGui_MouseCursor_ResizeAll
```
integer reaper.ImGui_MouseCursor_ResizeAll()
```

(Unused by Dear ImGui functions)
## ImGui_MouseCursor_ResizeEW
```
integer reaper.ImGui_MouseCursor_ResizeEW()
```

When hovering over a vertical border or a column.
## ImGui_MouseCursor_ResizeNESW
```
integer reaper.ImGui_MouseCursor_ResizeNESW()
```

When hovering over the bottom-left corner of a window.
## ImGui_MouseCursor_ResizeNS
```
integer reaper.ImGui_MouseCursor_ResizeNS()
```

When hovering over a horizontal border.
## ImGui_MouseCursor_ResizeNWSE
```
integer reaper.ImGui_MouseCursor_ResizeNWSE()
```

When hovering over the bottom-right corner of a window.
## ImGui_MouseCursor_TextInput
```
integer reaper.ImGui_MouseCursor_TextInput()
```

When hovering over InputText, etc.
## ImGui_NewLine
```
reaper.ImGui_NewLine(ImGui_Context ctx)
```

Undo a SameLine() or force a new line when in a horizontal-layout context.
## ImGui_NumericLimits_Double
```
number min, number max = reaper.ImGui_NumericLimits_Double()
```

Returns DBL_MIN and DBL_MAX for this system.
## ImGui_NumericLimits_Float
```
number min, number max = reaper.ImGui_NumericLimits_Float()
```

Returns FLT_MIN and FLT_MAX for this system.
## ImGui_NumericLimits_Int
```
integer min, integer max = reaper.ImGui_NumericLimits_Int()
```

Returns INT_MIN and INT_MAX for this system.
## ImGui_OpenPopup
```
reaper.ImGui_OpenPopup(ImGui_Context ctx, string str_id, optional integer popup_flagsIn)
```

Set popup state to open (don't call every frame!).
ImGuiPopupFlags are available for opening options.
## ImGui_OpenPopupOnItemClick
```
reaper.ImGui_OpenPopupOnItemClick(ImGui_Context ctx, optional string str_idIn, optional integer popup_flagsIn)
```

Helper to open popup when clicked on last item. return true when just opened.
(Note: actually triggers on the mouse _released_ event to be consistent with
popup behaviors.)
## ImGui_PlotHistogram
```
reaper.ImGui_PlotHistogram(ImGui_Context ctx, string label, reaper_array values, optional integer values_offsetIn, optional string overlay_textIn, optional number scale_minIn, optional number scale_maxIn, optional number graph_size_wIn, optional number graph_size_hIn)
```

No description available.
## ImGui_PlotLines
```
reaper.ImGui_PlotLines(ImGui_Context ctx, string label, reaper_array values, optional integer values_offsetIn, optional string overlay_textIn, optional number scale_minIn, optional number scale_maxIn, optional number graph_size_wIn, optional number graph_size_hIn)
```

No description available.
## ImGui_PointConvertNative
```
number x, number y = reaper.ImGui_PointConvertNative(ImGui_Context ctx, number x, number y, optional boolean to_nativeIn)
```

Convert a position from the current platform's native coordinate position
system to ReaImGui global coordinates (or vice versa).
## ImGui_PopButtonRepeat
```
reaper.ImGui_PopButtonRepeat(ImGui_Context ctx)
```

See PushButtonRepeat
## ImGui_PopClipRect
```
reaper.ImGui_PopClipRect(ImGui_Context ctx)
```

See PushClipRect
## ImGui_PopFont
```
reaper.ImGui_PopFont(ImGui_Context ctx)
```

See PushFont.
## ImGui_PopID
```
reaper.ImGui_PopID(ImGui_Context ctx)
```

Pop from the ID stack.
## ImGui_PopItemWidth
```
reaper.ImGui_PopItemWidth(ImGui_Context ctx)
```

See PushItemWidth
## ImGui_PopStyleColor
```
reaper.ImGui_PopStyleColor(ImGui_Context ctx, optional integer countIn)
```

No description available.
## ImGui_PopStyleVar
```
reaper.ImGui_PopStyleVar(ImGui_Context ctx, optional integer countIn)
```

Reset a style variable.
## ImGui_PopTabStop
```
reaper.ImGui_PopTabStop(ImGui_Context ctx)
```

See PushTabStop
## ImGui_PopTextWrapPos
```
reaper.ImGui_PopTextWrapPos(ImGui_Context ctx)
```

No description available.
## ImGui_PopupFlags_AnyPopup
```
integer reaper.ImGui_PopupFlags_AnyPopup()
```

PopupFlags_AnyPopupId | PopupFlags_AnyPopupLevel
## ImGui_PopupFlags_AnyPopupId
```
integer reaper.ImGui_PopupFlags_AnyPopupId()
```

Ignore the str_id parameter and test for any popup.
## ImGui_PopupFlags_AnyPopupLevel
```
integer reaper.ImGui_PopupFlags_AnyPopupLevel()
```

Search/test at any level of the popup stack (default test in the current level).
## ImGui_PopupFlags_MouseButtonLeft
```
integer reaper.ImGui_PopupFlags_MouseButtonLeft()
```

Open on Left Mouse release. Guaranteed to always be == 0 (same as MouseButton_Left).
## ImGui_PopupFlags_MouseButtonMiddle
```
integer reaper.ImGui_PopupFlags_MouseButtonMiddle()
```

Open on Middle Mouse release. Guaranteed to always be == 2 (same as MouseButton_Middle).
## ImGui_PopupFlags_MouseButtonRight
```
integer reaper.ImGui_PopupFlags_MouseButtonRight()
```

Open on Right Mouse release. Guaranteed to always be == 1 (same as MouseButton_Right).
## ImGui_PopupFlags_NoOpenOverExistingPopup
```
integer reaper.ImGui_PopupFlags_NoOpenOverExistingPopup()
```

Don't open if there's already a popup at the same level of the popup stack.
## ImGui_PopupFlags_NoOpenOverItems
```
integer reaper.ImGui_PopupFlags_NoOpenOverItems()
```

For BeginPopupContextWindow: don't return true when hovering items, only when hovering empty space.
## ImGui_PopupFlags_NoReopen
```
integer reaper.ImGui_PopupFlags_NoReopen()
```

Don't reopen same popup if already open (won't reposition, won't reinitialize navigation).
## ImGui_PopupFlags_None
```
integer reaper.ImGui_PopupFlags_None()
```

No description available.
## ImGui_ProgressBar
```
reaper.ImGui_ProgressBar(ImGui_Context ctx, number fraction, optional number size_arg_wIn, optional number size_arg_hIn, optional string overlayIn)
```

Fraction < 0.0 displays an indeterminate progress bar animation since v0.9.1.
The value must be animated along with time, for example `-1.0 * ImGui.GetTime()`.
## ImGui_PushButtonRepeat
```
reaper.ImGui_PushButtonRepeat(ImGui_Context ctx, boolean repeat)
```

In 'repeat' mode, Button*() functions return repeated true in a typematic
manner (using ConfigVar_KeyRepeatDelay/ConfigVar_KeyRepeatRate settings).
## ImGui_PushClipRect
```
reaper.ImGui_PushClipRect(ImGui_Context ctx, number clip_rect_min_x, number clip_rect_min_y, number clip_rect_max_x, number clip_rect_max_y, boolean intersect_with_current_clip_rect)
```

No description available.
## ImGui_PushFont
```
reaper.ImGui_PushFont(ImGui_Context ctx, ImGui_Font font)
```

Change the current font. Use nil to push the default font.
The font object must have been registered using Attach. See PopFont.
## ImGui_PushID
```
reaper.ImGui_PushID(ImGui_Context ctx, string str_id)
```

Push string into the ID stack.
## ImGui_PushItemWidth
```
reaper.ImGui_PushItemWidth(ImGui_Context ctx, number item_width)
```

Push width of items for common large "item+label" widgets.
## ImGui_PushStyleColor
```
reaper.ImGui_PushStyleColor(ImGui_Context ctx, integer idx, integer col_rgba)
```

Temporarily modify a style color.
Call PopStyleColor to undo after use (before the end of the frame).
See Col_* for available style colors.
## ImGui_PushStyleVar
```
reaper.ImGui_PushStyleVar(ImGui_Context ctx, integer var_idx, number val1, optional number val2In)
```

Temporarily modify a style variable.
Call PopStyleVar to undo after use (before the end of the frame).
See StyleVar_* for possible values of 'var_idx'.
## ImGui_PushTabStop
```
reaper.ImGui_PushTabStop(ImGui_Context ctx, boolean tab_stop)
```

Allow focusing using TAB/Shift-TAB, enabled by default but you can disable it
for certain widgets
## ImGui_PushTextWrapPos
```
reaper.ImGui_PushTextWrapPos(ImGui_Context ctx, optional number wrap_local_pos_xIn)
```

Push word-wrapping position for Text*() commands.
## ImGui_RadioButton
```
boolean reaper.ImGui_RadioButton(ImGui_Context ctx, string label, boolean active)
```

Use with e.g. if (RadioButton("one", my_value==1)) { my_value = 1; }
## ImGui_RadioButtonEx
```
boolean retval, integer v = reaper.ImGui_RadioButtonEx(ImGui_Context ctx, string label, integer v, integer v_button)
```

Shortcut to handle RadioButton's example pattern when value is an integer
## ImGui_ResetMouseDragDelta
```
reaper.ImGui_ResetMouseDragDelta(ImGui_Context ctx, optional integer buttonIn)
```

No description available.
## ImGui_SameLine
```
reaper.ImGui_SameLine(ImGui_Context ctx, optional number offset_from_start_xIn, optional number spacingIn)
```

Call between widgets or groups to layout them horizontally.
X position given in window coordinates.
## ImGui_Selectable
```
boolean retval, optional boolean p_selected = reaper.ImGui_Selectable(ImGui_Context ctx, string label, optional boolean p_selected, optional integer flagsIn, optional number size_wIn, optional number size_hIn)
```

No description available.
## ImGui_SelectableFlags_AllowDoubleClick
```
integer reaper.ImGui_SelectableFlags_AllowDoubleClick()
```

Generate press events on double clicks too.
## ImGui_SelectableFlags_AllowOverlap
```
integer reaper.ImGui_SelectableFlags_AllowOverlap()
```

Hit testing to allow subsequent widgets to overlap this one.
## ImGui_SelectableFlags_Disabled
```
integer reaper.ImGui_SelectableFlags_Disabled()
```

Cannot be selected, display grayed out text.
## ImGui_SelectableFlags_DontClosePopups
```
integer reaper.ImGui_SelectableFlags_DontClosePopups()
```

Clicking this doesn't close parent popup window.
## ImGui_SelectableFlags_None
```
integer reaper.ImGui_SelectableFlags_None()
```

No description available.
## ImGui_SelectableFlags_SpanAllColumns
```
integer reaper.ImGui_SelectableFlags_SpanAllColumns()
```

Frame will span all columns of its container table (text will still fit in current column).
## ImGui_Separator
```
reaper.ImGui_Separator(ImGui_Context ctx)
```

Separator, generally horizontal. inside a menu bar or in horizontal layout
mode, this becomes a vertical separator.
## ImGui_SeparatorText
```
reaper.ImGui_SeparatorText(ImGui_Context ctx, string label)
```

Text formatted with an horizontal line
## ImGui_SetClipboardText
```
reaper.ImGui_SetClipboardText(ImGui_Context ctx, string text)
```

See also the LogToClipboard function to capture GUI into clipboard,
or easily output text data to the clipboard.
## ImGui_SetColorEditOptions
```
reaper.ImGui_SetColorEditOptions(ImGui_Context ctx, integer flags)
```

Picker type, etc. User will be able to change many settings, unless you pass
the _NoOptions flag to your calls.
## ImGui_SetConfigVar
```
reaper.ImGui_SetConfigVar(ImGui_Context ctx, integer var_idx, number value)
```

No description available.
## ImGui_SetCursorPos
```
reaper.ImGui_SetCursorPos(ImGui_Context ctx, number local_pos_x, number local_pos_y)
```

Cursor position in window
## ImGui_SetCursorPosX
```
reaper.ImGui_SetCursorPosX(ImGui_Context ctx, number local_x)
```

Cursor X position in window
## ImGui_SetCursorPosY
```
reaper.ImGui_SetCursorPosY(ImGui_Context ctx, number local_y)
```

Cursor Y position in window
## ImGui_SetCursorScreenPos
```
reaper.ImGui_SetCursorScreenPos(ImGui_Context ctx, number pos_x, number pos_y)
```

Cursor position in absolute screen coordinates.
## ImGui_SetDragDropPayload
```
boolean reaper.ImGui_SetDragDropPayload(ImGui_Context ctx, string type, string data, optional integer condIn)
```

The type is a user defined string of maximum 32 characters.
Strings starting with '_' are reserved for dear imgui internal types.
Data is copied and held by imgui.
## ImGui_SetItemDefaultFocus
```
reaper.ImGui_SetItemDefaultFocus(ImGui_Context ctx)
```

Make last item the default focused item of a window.
## ImGui_SetItemTooltip
```
reaper.ImGui_SetItemTooltip(ImGui_Context ctx, string text)
```

Set a text-only tooltip if preceding item was hovered.
Override any previous call to SetTooltip(). Shortcut for
`if (IsItemHovered(HoveredFlags_ForTooltip)) { SetTooltip(...); }`.
## ImGui_SetKeyboardFocusHere
```
reaper.ImGui_SetKeyboardFocusHere(ImGui_Context ctx, optional integer offsetIn)
```

Focus keyboard on the next widget. Use positive 'offset' to access sub
components of a multiple component widget. Use -1 to access previous widget.
## ImGui_SetMouseCursor
```
reaper.ImGui_SetMouseCursor(ImGui_Context ctx, integer cursor_type)
```

Set desired mouse cursor shape. See MouseCursor_* for possible values.
## ImGui_SetNextFrameWantCaptureKeyboard
```
reaper.ImGui_SetNextFrameWantCaptureKeyboard(ImGui_Context ctx, boolean want_capture_keyboard)
```

Request capture of keyboard shortcuts in REAPER's global scope for the next frame.
## ImGui_SetNextItemAllowOverlap
```
reaper.ImGui_SetNextItemAllowOverlap(ImGui_Context ctx)
```

Allow next item to be overlapped by a subsequent item.
Useful with invisible buttons, selectable, treenode covering an area where
subsequent items may need to be added. Note that both Selectable() and TreeNode()
have dedicated flags doing this.
## ImGui_SetNextItemOpen
```
reaper.ImGui_SetNextItemOpen(ImGui_Context ctx, boolean is_open, optional integer condIn)
```

Set next TreeNode/CollapsingHeader open state.
Can also be done with the TreeNodeFlags_DefaultOpen flag.
## ImGui_SetNextItemShortcut
```
reaper.ImGui_SetNextItemShortcut(ImGui_Context ctx, integer key_chord, optional integer flagsIn)
```

No description available.
## ImGui_SetNextItemWidth
```
reaper.ImGui_SetNextItemWidth(ImGui_Context ctx, number item_width)
```

Set width of the _next_ common large "item+label" widget.
## ImGui_SetNextWindowBgAlpha
```
reaper.ImGui_SetNextWindowBgAlpha(ImGui_Context ctx, number alpha)
```

Set next window background color alpha. Helper to easily override the Alpha
component of Col_WindowBg/Col_ChildBg/Col_PopupBg.
You may also use WindowFlags_NoBackground for a fully transparent window.
## ImGui_SetNextWindowCollapsed
```
reaper.ImGui_SetNextWindowCollapsed(ImGui_Context ctx, boolean collapsed, optional integer condIn)
```

Set next window collapsed state.
## ImGui_SetNextWindowContentSize
```
reaper.ImGui_SetNextWindowContentSize(ImGui_Context ctx, number size_w, number size_h)
```

Set next window content size (~ scrollable client area, which enforce the
range of scrollbars). Not including window decorations (title bar, menu bar,
etc.) nor StyleVar_WindowPadding. set an axis to 0.0 to leave it automatic.
## ImGui_SetNextWindowDockID
```
reaper.ImGui_SetNextWindowDockID(ImGui_Context ctx, integer dock_id, optional integer condIn)
```

No description available.
## ImGui_SetNextWindowFocus
```
reaper.ImGui_SetNextWindowFocus(ImGui_Context ctx)
```

Set next window to be focused / top-most.
## ImGui_SetNextWindowPos
```
reaper.ImGui_SetNextWindowPos(ImGui_Context ctx, number pos_x, number pos_y, optional integer condIn, optional number pivot_xIn, optional number pivot_yIn)
```

Set next window position. Use pivot=(0.5,0.5) to center on given point, etc.
## ImGui_SetNextWindowScroll
```
reaper.ImGui_SetNextWindowScroll(ImGui_Context ctx, number scroll_x, number scroll_y)
```

Set next window scrolling value (use < 0.0 to not affect a given axis).
## ImGui_SetNextWindowSize
```
reaper.ImGui_SetNextWindowSize(ImGui_Context ctx, number size_w, number size_h, optional integer condIn)
```

Set next window size. set axis to 0.0 to force an auto-fit on this axis.
## ImGui_SetNextWindowSizeConstraints
```
reaper.ImGui_SetNextWindowSizeConstraints(ImGui_Context ctx, number size_min_w, number size_min_h, number size_max_w, number size_max_h, ImGui_Function custom_callbackIn)
```

Set next window size limits. Use 0.0 or FLT_MAX (second return value of
NumericLimits_Float) if you don't want limits.
## ImGui_SetScrollFromPosX
```
reaper.ImGui_SetScrollFromPosX(ImGui_Context ctx, number local_x, optional number center_x_ratioIn)
```

Adjust scrolling amount to make given position visible.
Generally GetCursorStartPos() + offset to compute a valid position.
## ImGui_SetScrollFromPosY
```
reaper.ImGui_SetScrollFromPosY(ImGui_Context ctx, number local_y, optional number center_y_ratioIn)
```

Adjust scrolling amount to make given position visible.
Generally GetCursorStartPos() + offset to compute a valid position.
## ImGui_SetScrollHereX
```
reaper.ImGui_SetScrollHereX(ImGui_Context ctx, optional number center_x_ratioIn)
```

Adjust scrolling amount to make current cursor position visible.
center_x_ratio=0.0: left, 0.5: center, 1.0: right.
When using to make a "default/current item" visible,
consider using SetItemDefaultFocus instead.
## ImGui_SetScrollHereY
```
reaper.ImGui_SetScrollHereY(ImGui_Context ctx, optional number center_y_ratioIn)
```

Adjust scrolling amount to make current cursor position visible.
center_y_ratio=0.0: top, 0.5: center, 1.0: bottom.
When using to make a "default/current item" visible,
consider using SetItemDefaultFocus instead.
## ImGui_SetScrollX
```
reaper.ImGui_SetScrollX(ImGui_Context ctx, number scroll_x)
```

Set scrolling amount [0 .. GetScrollMaxX()]
## ImGui_SetScrollY
```
reaper.ImGui_SetScrollY(ImGui_Context ctx, number scroll_y)
```

Set scrolling amount [0 .. GetScrollMaxY()]
## ImGui_SetTabItemClosed
```
reaper.ImGui_SetTabItemClosed(ImGui_Context ctx, string tab_or_docked_window_label)
```

Notify TabBar or Docking system of a closed tab/window ahead
(useful to reduce visual flicker on reorderable tab bars).
For tab-bar: call after BeginTabBar and before Tab submissions.
Otherwise call with a window name.
## ImGui_SetTooltip
```
reaper.ImGui_SetTooltip(ImGui_Context ctx, string text)
```

Set a text-only tooltip. Often used after a IsItemHovered() check.
Override any previous call to SetTooltip.
## ImGui_SetWindowCollapsed
```
reaper.ImGui_SetWindowCollapsed(ImGui_Context ctx, boolean collapsed, optional integer condIn)
```

(Not recommended) Set current window collapsed state.
Prefer using SetNextWindowCollapsed.
## ImGui_SetWindowCollapsedEx
```
reaper.ImGui_SetWindowCollapsedEx(ImGui_Context ctx, string name, boolean collapsed, optional integer condIn)
```

Set named window collapsed state.
## ImGui_SetWindowFocus
```
reaper.ImGui_SetWindowFocus(ImGui_Context ctx)
```

(Not recommended) Set current window to be focused / top-most.
Prefer using SetNextWindowFocus.
## ImGui_SetWindowFocusEx
```
reaper.ImGui_SetWindowFocusEx(ImGui_Context ctx, string name)
```

Set named window to be focused / top-most. Use an empty name to remove focus.
## ImGui_SetWindowPos
```
reaper.ImGui_SetWindowPos(ImGui_Context ctx, number pos_x, number pos_y, optional integer condIn)
```

(Not recommended) Set current window position - call within Begin/End.
Prefer using SetNextWindowPos, as this may incur tearing and minor side-effects.
## ImGui_SetWindowPosEx
```
reaper.ImGui_SetWindowPosEx(ImGui_Context ctx, string name, number pos_x, number pos_y, optional integer condIn)
```

Set named window position.
## ImGui_SetWindowSize
```
reaper.ImGui_SetWindowSize(ImGui_Context ctx, number size_w, number size_h, optional integer condIn)
```

(Not recommended) Set current window size - call within Begin/End.
Set size_w and size_h to 0 to force an auto-fit.
Prefer using SetNextWindowSize, as this may incur tearing and minor side-effects.
## ImGui_SetWindowSizeEx
```
reaper.ImGui_SetWindowSizeEx(ImGui_Context ctx, string name, number size_w, number size_h, optional integer condIn)
```

Set named window size. Set axis to 0.0 to force an auto-fit on this axis.
## ImGui_Shortcut
```
boolean reaper.ImGui_Shortcut(ImGui_Context ctx, integer key_chord, optional integer flagsIn)
```

No description available.
## ImGui_ShowAboutWindow
```
optional boolean p_open = reaper.ImGui_ShowAboutWindow(ImGui_Context ctx, optional boolean p_open)
```

Create About window.
Display ReaImGui version, Dear ImGui version, credits and build/system information.
## ImGui_ShowDebugLogWindow
```
optional boolean p_open = reaper.ImGui_ShowDebugLogWindow(ImGui_Context ctx, optional boolean p_open)
```

Create Debug Log window. display a simplified log of important dear imgui events.
## ImGui_ShowIDStackToolWindow
```
optional boolean p_open = reaper.ImGui_ShowIDStackToolWindow(ImGui_Context ctx, optional boolean p_open)
```

Create Stack Tool window. Hover items with mouse to query information about
the source of their unique ID.
## ImGui_ShowMetricsWindow
```
optional boolean p_open = reaper.ImGui_ShowMetricsWindow(ImGui_Context ctx, optional boolean p_open)
```

Create Metrics/Debugger window.
Display Dear ImGui internals: windows, draw commands, various internal state, etc.
## ImGui_SliderAngle
```
boolean retval, number v_rad = reaper.ImGui_SliderAngle(ImGui_Context ctx, string label, number v_rad, optional number v_degrees_minIn, optional number v_degrees_maxIn, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_SliderDouble
```
boolean retval, number v = reaper.ImGui_SliderDouble(ImGui_Context ctx, string label, number v, number v_min, number v_max, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_SliderDouble2
```
boolean retval, number v1, number v2 = reaper.ImGui_SliderDouble2(ImGui_Context ctx, string label, number v1, number v2, number v_min, number v_max, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_SliderDouble3
```
boolean retval, number v1, number v2, number v3 = reaper.ImGui_SliderDouble3(ImGui_Context ctx, string label, number v1, number v2, number v3, number v_min, number v_max, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_SliderDouble4
```
boolean retval, number v1, number v2, number v3, number v4 = reaper.ImGui_SliderDouble4(ImGui_Context ctx, string label, number v1, number v2, number v3, number v4, number v_min, number v_max, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_SliderDoubleN
```
boolean reaper.ImGui_SliderDoubleN(ImGui_Context ctx, string label, reaper_array values, number v_min, number v_max, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_SliderFlags_AlwaysClamp
```
integer reaper.ImGui_SliderFlags_AlwaysClamp()
```

Clamp value to min/max bounds when input manually with CTRL+Click. By default CTRL+Click allows going out of bounds.
## ImGui_SliderFlags_Logarithmic
```
integer reaper.ImGui_SliderFlags_Logarithmic()
```

Make the widget logarithmic (linear otherwise). Consider using SliderFlags_NoRoundToFormat with this if using a format-string with small amount of digits.
## ImGui_SliderFlags_NoInput
```
integer reaper.ImGui_SliderFlags_NoInput()
```

Disable CTRL+Click or Enter key allowing to input text directly into the widget.
## ImGui_SliderFlags_NoRoundToFormat
```
integer reaper.ImGui_SliderFlags_NoRoundToFormat()
```

Disable rounding underlying value to match precision of the display format string (e.g. %.3f values are rounded to those 3 digits).
## ImGui_SliderFlags_None
```
integer reaper.ImGui_SliderFlags_None()
```

No description available.
## ImGui_SliderFlags_WrapAround
```
integer reaper.ImGui_SliderFlags_WrapAround()
```

Enable wrapping around from max to min and from min to max (only supported by DragXXX() functions for now).
## ImGui_SliderInt
```
boolean retval, integer v = reaper.ImGui_SliderInt(ImGui_Context ctx, string label, integer v, integer v_min, integer v_max, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_SliderInt2
```
boolean retval, integer v1, integer v2 = reaper.ImGui_SliderInt2(ImGui_Context ctx, string label, integer v1, integer v2, integer v_min, integer v_max, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_SliderInt3
```
boolean retval, integer v1, integer v2, integer v3 = reaper.ImGui_SliderInt3(ImGui_Context ctx, string label, integer v1, integer v2, integer v3, integer v_min, integer v_max, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_SliderInt4
```
boolean retval, integer v1, integer v2, integer v3, integer v4 = reaper.ImGui_SliderInt4(ImGui_Context ctx, string label, integer v1, integer v2, integer v3, integer v4, integer v_min, integer v_max, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_SmallButton
```
boolean reaper.ImGui_SmallButton(ImGui_Context ctx, string label)
```

Button with StyleVar_FramePadding.y == 0 to easily embed within text.
## ImGui_SortDirection_Ascending
```
integer reaper.ImGui_SortDirection_Ascending()
```

Ascending = 0->9, A->Z etc.
## ImGui_SortDirection_Descending
```
integer reaper.ImGui_SortDirection_Descending()
```

Descending = 9->0, Z->A etc.
## ImGui_SortDirection_None
```
integer reaper.ImGui_SortDirection_None()
```

No description available.
## ImGui_Spacing
```
reaper.ImGui_Spacing(ImGui_Context ctx)
```

Add vertical spacing.
## ImGui_StyleVar_Alpha
```
integer reaper.ImGui_StyleVar_Alpha()
```

Global alpha applies to everything in Dear ImGui.
## ImGui_StyleVar_ButtonTextAlign
```
integer reaper.ImGui_StyleVar_ButtonTextAlign()
```

Alignment of button text when button is larger than text. Defaults to (0.5, 0.5) (centered).
## ImGui_StyleVar_CellPadding
```
integer reaper.ImGui_StyleVar_CellPadding()
```

Padding within a table cell. CellPadding.x is locked for entire table. CellPadding.y may be altered between different rows.
## ImGui_StyleVar_ChildBorderSize
```
integer reaper.ImGui_StyleVar_ChildBorderSize()
```

Thickness of border around child windows. Generally set to 0.0 or 1.0. (Other values are not well tested and more CPU/GPU costly).
## ImGui_StyleVar_ChildRounding
```
integer reaper.ImGui_StyleVar_ChildRounding()
```

Radius of child window corners rounding. Set to 0.0 to have rectangular windows.
## ImGui_StyleVar_DisabledAlpha
```
integer reaper.ImGui_StyleVar_DisabledAlpha()
```

Additional alpha multiplier applied by BeginDisabled. Multiply over current value of Alpha.
## ImGui_StyleVar_FrameBorderSize
```
integer reaper.ImGui_StyleVar_FrameBorderSize()
```

Thickness of border around frames. Generally set to 0.0 or 1.0. (Other values are not well tested and more CPU/GPU costly).
## ImGui_StyleVar_FramePadding
```
integer reaper.ImGui_StyleVar_FramePadding()
```

Padding within a framed rectangle (used by most widgets).
## ImGui_StyleVar_FrameRounding
```
integer reaper.ImGui_StyleVar_FrameRounding()
```

Radius of frame corners rounding. Set to 0.0 to have rectangular frame (used by most widgets).
## ImGui_StyleVar_GrabMinSize
```
integer reaper.ImGui_StyleVar_GrabMinSize()
```

Minimum width/height of a grab box for slider/scrollbar.
## ImGui_StyleVar_GrabRounding
```
integer reaper.ImGui_StyleVar_GrabRounding()
```

Radius of grabs corners rounding. Set to 0.0 to have rectangular slider grabs.
## ImGui_StyleVar_IndentSpacing
```
integer reaper.ImGui_StyleVar_IndentSpacing()
```

Horizontal indentation when e.g. entering a tree node. Generally == (GetFontSize + StyleVar_FramePadding.x*2).
## ImGui_StyleVar_ItemInnerSpacing
```
integer reaper.ImGui_StyleVar_ItemInnerSpacing()
```

Horizontal and vertical spacing between within elements of a composed widget (e.g. a slider and its label).
## ImGui_StyleVar_ItemSpacing
```
integer reaper.ImGui_StyleVar_ItemSpacing()
```

Horizontal and vertical spacing between widgets/lines.
## ImGui_StyleVar_PopupBorderSize
```
integer reaper.ImGui_StyleVar_PopupBorderSize()
```

Thickness of border around popup/tooltip windows. Generally set to 0.0 or 1.0. (Other values are not well tested and more CPU/GPU costly).
## ImGui_StyleVar_PopupRounding
```
integer reaper.ImGui_StyleVar_PopupRounding()
```

Radius of popup window corners rounding. (Note that tooltip windows use StyleVar_WindowRounding.)
## ImGui_StyleVar_ScrollbarRounding
```
integer reaper.ImGui_StyleVar_ScrollbarRounding()
```

Radius of grab corners for scrollbar.
## ImGui_StyleVar_ScrollbarSize
```
integer reaper.ImGui_StyleVar_ScrollbarSize()
```

Width of the vertical scrollbar, Height of the horizontal scrollbar.
## ImGui_StyleVar_SelectableTextAlign
```
integer reaper.ImGui_StyleVar_SelectableTextAlign()
```

Alignment of selectable text. Defaults to (0.0, 0.0) (top-left aligned). It's generally important to keep this left-aligned if you want to lay multiple items on a same line.
## ImGui_StyleVar_SeparatorTextAlign
```
integer reaper.ImGui_StyleVar_SeparatorTextAlign()
```

Alignment of text within the separator.
Defaults to (0.0, 0.5) (left aligned, center).
## ImGui_StyleVar_SeparatorTextBorderSize
```
integer reaper.ImGui_StyleVar_SeparatorTextBorderSize()
```

Thickness of border in SeparatorText()
## ImGui_StyleVar_SeparatorTextPadding
```
integer reaper.ImGui_StyleVar_SeparatorTextPadding()
```

Horizontal offset of text from each edge of the separator + spacing on other
axis. Generally small values. .y is recommended to be == StyleVar_FramePadding.y.
## ImGui_StyleVar_TabBarBorderSize
```
integer reaper.ImGui_StyleVar_TabBarBorderSize()
```

Thickness of tab-bar separator, which takes on the tab active color to denote focus.
## ImGui_StyleVar_TabBorderSize
```
integer reaper.ImGui_StyleVar_TabBorderSize()
```

Thickness of border around tabs.
## ImGui_StyleVar_TabRounding
```
integer reaper.ImGui_StyleVar_TabRounding()
```

Radius of upper corners of a tab. Set to 0.0 to have rectangular tabs.
## ImGui_StyleVar_TableAngledHeadersAngle
```
integer reaper.ImGui_StyleVar_TableAngledHeadersAngle()
```

Angle of angled headers (supported values range from -50.0 degrees to +50.0 degrees).
## ImGui_StyleVar_TableAngledHeadersTextAlign
```
integer reaper.ImGui_StyleVar_TableAngledHeadersTextAlign()
```

Alignment of angled headers within the cell
## ImGui_StyleVar_WindowBorderSize
```
integer reaper.ImGui_StyleVar_WindowBorderSize()
```

Thickness of border around windows. Generally set to 0.0 or 1.0. (Other values are not well tested and more CPU/GPU costly).
## ImGui_StyleVar_WindowMinSize
```
integer reaper.ImGui_StyleVar_WindowMinSize()
```

Minimum window size. This is a global setting. If you want to constrain individual windows, use SetNextWindowSizeConstraints.
## ImGui_StyleVar_WindowPadding
```
integer reaper.ImGui_StyleVar_WindowPadding()
```

Padding within a window.
## ImGui_StyleVar_WindowRounding
```
integer reaper.ImGui_StyleVar_WindowRounding()
```

Radius of window corners rounding. Set to 0.0 to have rectangular windows. Large values tend to lead to variety of artifacts and are not recommended.
## ImGui_StyleVar_WindowTitleAlign
```
integer reaper.ImGui_StyleVar_WindowTitleAlign()
```

Alignment for title bar text. Defaults to (0.0,0.5) for left-aligned,vertically centered.
## ImGui_TabBarFlags_AutoSelectNewTabs
```
integer reaper.ImGui_TabBarFlags_AutoSelectNewTabs()
```

Automatically select new tabs when they appear.
## ImGui_TabBarFlags_DrawSelectedOverline
```
integer reaper.ImGui_TabBarFlags_DrawSelectedOverline()
```

Draw selected overline markers over selected tab
## ImGui_TabBarFlags_FittingPolicyResizeDown
```
integer reaper.ImGui_TabBarFlags_FittingPolicyResizeDown()
```

Resize tabs when they don't fit.
## ImGui_TabBarFlags_FittingPolicyScroll
```
integer reaper.ImGui_TabBarFlags_FittingPolicyScroll()
```

Add scroll buttons when tabs don't fit.
## ImGui_TabBarFlags_NoCloseWithMiddleMouseButton
```
integer reaper.ImGui_TabBarFlags_NoCloseWithMiddleMouseButton()
```

Disable behavior of closing tabs (that are submitted with p_open != nil) with middle mouse button. You may handle this behavior manually on user's side with if(IsItemHovered() && IsMouseClicked(2)) p_open = false.
## ImGui_TabBarFlags_NoTabListScrollingButtons
```
integer reaper.ImGui_TabBarFlags_NoTabListScrollingButtons()
```

Disable scrolling buttons (apply when fitting policy is TabBarFlags_FittingPolicyScroll).
## ImGui_TabBarFlags_NoTooltip
```
integer reaper.ImGui_TabBarFlags_NoTooltip()
```

Disable tooltips when hovering a tab.
## ImGui_TabBarFlags_None
```
integer reaper.ImGui_TabBarFlags_None()
```

No description available.
## ImGui_TabBarFlags_Reorderable
```
integer reaper.ImGui_TabBarFlags_Reorderable()
```

Allow manually dragging tabs to re-order them + New tabs are appended at the end of list.
## ImGui_TabBarFlags_TabListPopupButton
```
integer reaper.ImGui_TabBarFlags_TabListPopupButton()
```

Disable buttons to open the tab list popup.
## ImGui_TabItemButton
```
boolean reaper.ImGui_TabItemButton(ImGui_Context ctx, string label, optional integer flagsIn)
```

Create a Tab behaving like a button. Return true when clicked.
Cannot be selected in the tab bar.
## ImGui_TabItemFlags_Leading
```
integer reaper.ImGui_TabItemFlags_Leading()
```

Enforce the tab position to the left of the tab bar (after the tab list popup button).
## ImGui_TabItemFlags_NoAssumedClosure
```
integer reaper.ImGui_TabItemFlags_NoAssumedClosure()
```

Tab is selected when trying to close + closure is not immediately assumed (will wait for user to stop submitting the tab). Otherwise closure is assumed when pressing the X, so if you keep submitting the tab may reappear at end of tab bar.
## ImGui_TabItemFlags_NoCloseWithMiddleMouseButton
```
integer reaper.ImGui_TabItemFlags_NoCloseWithMiddleMouseButton()
```

Disable behavior of closing tabs (that are submitted with p_open != nil) with middle mouse button. You can still repro this behavior on user's side with if(IsItemHovered() && IsMouseClicked(2)) p_open = false.
## ImGui_TabItemFlags_NoPushId
```
integer reaper.ImGui_TabItemFlags_NoPushId()
```

Don't call PushID()/PopID() on BeginTabItem/EndTabItem.
## ImGui_TabItemFlags_NoReorder
```
integer reaper.ImGui_TabItemFlags_NoReorder()
```

Disable reordering this tab or having another tab cross over this tab.
## ImGui_TabItemFlags_NoTooltip
```
integer reaper.ImGui_TabItemFlags_NoTooltip()
```

Disable tooltip for the given tab.
## ImGui_TabItemFlags_None
```
integer reaper.ImGui_TabItemFlags_None()
```

No description available.
## ImGui_TabItemFlags_SetSelected
```
integer reaper.ImGui_TabItemFlags_SetSelected()
```

Trigger flag to programmatically make the tab selected when calling BeginTabItem.
## ImGui_TabItemFlags_Trailing
```
integer reaper.ImGui_TabItemFlags_Trailing()
```

Enforce the tab position to the right of the tab bar (before the scrolling buttons).
## ImGui_TabItemFlags_UnsavedDocument
```
integer reaper.ImGui_TabItemFlags_UnsavedDocument()
```

Display a dot next to the title + set TabItemFlags_NoAssumedClosure.
## ImGui_TableAngledHeadersRow
```
reaper.ImGui_TableAngledHeadersRow(ImGui_Context ctx)
```

Submit a row with angled headers for every column with the
TableColumnFlags_AngledHeader flag. Must be the first row.
## ImGui_TableBgTarget_CellBg
```
integer reaper.ImGui_TableBgTarget_CellBg()
```

Set cell background color (top-most color).
## ImGui_TableBgTarget_None
```
integer reaper.ImGui_TableBgTarget_None()
```

No description available.
## ImGui_TableBgTarget_RowBg0
```
integer reaper.ImGui_TableBgTarget_RowBg0()
```

Set row background color 0 (generally used for background, automatically set when TableFlags_RowBg is used).
## ImGui_TableBgTarget_RowBg1
```
integer reaper.ImGui_TableBgTarget_RowBg1()
```

Set row background color 1 (generally used for selection marking).
## ImGui_TableColumnFlags_AngledHeader
```
integer reaper.ImGui_TableColumnFlags_AngledHeader()
```

TableHeadersRow will submit an angled header row for this column. Note this will add an extra row.
## ImGui_TableColumnFlags_DefaultHide
```
integer reaper.ImGui_TableColumnFlags_DefaultHide()
```

Default as a hidden/disabled column.
## ImGui_TableColumnFlags_DefaultSort
```
integer reaper.ImGui_TableColumnFlags_DefaultSort()
```

Default as a sorting column.
## ImGui_TableColumnFlags_Disabled
```
integer reaper.ImGui_TableColumnFlags_Disabled()
```

Overriding/master disable flag: hide column, won't show in context menu (unlike calling TableSetColumnEnabled which manipulates the user accessible state).
## ImGui_TableColumnFlags_IndentDisable
```
integer reaper.ImGui_TableColumnFlags_IndentDisable()
```

Ignore current Indent value when entering cell (default for columns > 0). Indentation changes _within_ the cell will still be honored.
## ImGui_TableColumnFlags_IndentEnable
```
integer reaper.ImGui_TableColumnFlags_IndentEnable()
```

Use current Indent value when entering cell (default for column 0).
## ImGui_TableColumnFlags_IsEnabled
```
integer reaper.ImGui_TableColumnFlags_IsEnabled()
```

Status: is enabled == not hidden by user/api (referred to as "Hide" in _DefaultHide and _NoHide) flags.
## ImGui_TableColumnFlags_IsHovered
```
integer reaper.ImGui_TableColumnFlags_IsHovered()
```

Status: is hovered by mouse.
## ImGui_TableColumnFlags_IsSorted
```
integer reaper.ImGui_TableColumnFlags_IsSorted()
```

Status: is currently part of the sort specs.
## ImGui_TableColumnFlags_IsVisible
```
integer reaper.ImGui_TableColumnFlags_IsVisible()
```

Status: is visible == is enabled AND not clipped by scrolling.
## ImGui_TableColumnFlags_NoClip
```
integer reaper.ImGui_TableColumnFlags_NoClip()
```

Disable clipping for this column (all NoClip columns will render in a same draw command).
## ImGui_TableColumnFlags_NoHeaderLabel
```
integer reaper.ImGui_TableColumnFlags_NoHeaderLabel()
```

TableHeadersRow will not submit horizontal label for this column. Convenient for some small columns. Name will still appear in context menu or in angled headers.
## ImGui_TableColumnFlags_NoHeaderWidth
```
integer reaper.ImGui_TableColumnFlags_NoHeaderWidth()
```

Disable header text width contribution to automatic column width.
## ImGui_TableColumnFlags_NoHide
```
integer reaper.ImGui_TableColumnFlags_NoHide()
```

Disable ability to hide/disable this column.
## ImGui_TableColumnFlags_NoReorder
```
integer reaper.ImGui_TableColumnFlags_NoReorder()
```

Disable manual reordering this column, this will also prevent other columns from crossing over this column.
## ImGui_TableColumnFlags_NoResize
```
integer reaper.ImGui_TableColumnFlags_NoResize()
```

Disable manual resizing.
## ImGui_TableColumnFlags_NoSort
```
integer reaper.ImGui_TableColumnFlags_NoSort()
```

Disable ability to sort on this field (even if TableFlags_Sortable is set on the table).
## ImGui_TableColumnFlags_NoSortAscending
```
integer reaper.ImGui_TableColumnFlags_NoSortAscending()
```

Disable ability to sort in the ascending direction.
## ImGui_TableColumnFlags_NoSortDescending
```
integer reaper.ImGui_TableColumnFlags_NoSortDescending()
```

Disable ability to sort in the descending direction.
## ImGui_TableColumnFlags_None
```
integer reaper.ImGui_TableColumnFlags_None()
```

No description available.
## ImGui_TableColumnFlags_PreferSortAscending
```
integer reaper.ImGui_TableColumnFlags_PreferSortAscending()
```

Make the initial sort direction Ascending when first sorting on this column (default).
## ImGui_TableColumnFlags_PreferSortDescending
```
integer reaper.ImGui_TableColumnFlags_PreferSortDescending()
```

Make the initial sort direction Descending when first sorting on this column.
## ImGui_TableColumnFlags_WidthFixed
```
integer reaper.ImGui_TableColumnFlags_WidthFixed()
```

Column will not stretch. Preferable with horizontal scrolling enabled (default if table sizing policy is _SizingFixedFit and table is resizable).
## ImGui_TableColumnFlags_WidthStretch
```
integer reaper.ImGui_TableColumnFlags_WidthStretch()
```

Column will stretch. Preferable with horizontal scrolling disabled (default if table sizing policy is _SizingStretchSame or _SizingStretchProp).
## ImGui_TableFlags_Borders
```
integer reaper.ImGui_TableFlags_Borders()
```

Draw all borders.
## ImGui_TableFlags_BordersH
```
integer reaper.ImGui_TableFlags_BordersH()
```

Draw horizontal borders.
## ImGui_TableFlags_BordersInner
```
integer reaper.ImGui_TableFlags_BordersInner()
```

Draw inner borders.
## ImGui_TableFlags_BordersInnerH
```
integer reaper.ImGui_TableFlags_BordersInnerH()
```

Draw horizontal borders between rows.
## ImGui_TableFlags_BordersInnerV
```
integer reaper.ImGui_TableFlags_BordersInnerV()
```

Draw vertical borders between columns.
## ImGui_TableFlags_BordersOuter
```
integer reaper.ImGui_TableFlags_BordersOuter()
```

Draw outer borders.
## ImGui_TableFlags_BordersOuterH
```
integer reaper.ImGui_TableFlags_BordersOuterH()
```

Draw horizontal borders at the top and bottom.
## ImGui_TableFlags_BordersOuterV
```
integer reaper.ImGui_TableFlags_BordersOuterV()
```

Draw vertical borders on the left and right sides.
## ImGui_TableFlags_BordersV
```
integer reaper.ImGui_TableFlags_BordersV()
```

Draw vertical borders.
## ImGui_TableFlags_ContextMenuInBody
```
integer reaper.ImGui_TableFlags_ContextMenuInBody()
```

Right-click on columns body/contents will display table context menu. By default it is available in TableHeadersRow.
## ImGui_TableFlags_Hideable
```
integer reaper.ImGui_TableFlags_Hideable()
```

Enable hiding/disabling columns in context menu.
## ImGui_TableFlags_HighlightHoveredColumn
```
integer reaper.ImGui_TableFlags_HighlightHoveredColumn()
```

Highlight column headers when hovered (may evolve into a fuller highlight.)
## ImGui_TableFlags_NoClip
```
integer reaper.ImGui_TableFlags_NoClip()
```

Disable clipping rectangle for every individual columns (reduce draw command count, items will be able to overflow into other columns). Generally incompatible with TableSetupScrollFreeze.
## ImGui_TableFlags_NoHostExtendX
```
integer reaper.ImGui_TableFlags_NoHostExtendX()
```

Make outer width auto-fit to columns, overriding outer_size.x value. Only available when ScrollX/ScrollY are disabled and Stretch columns are not used.
## ImGui_TableFlags_NoHostExtendY
```
integer reaper.ImGui_TableFlags_NoHostExtendY()
```

Make outer height stop exactly at outer_size.y (prevent auto-extending table past the limit). Only available when ScrollX/ScrollY are disabled. Data below the limit will be clipped and not visible.
## ImGui_TableFlags_NoKeepColumnsVisible
```
integer reaper.ImGui_TableFlags_NoKeepColumnsVisible()
```

Disable keeping column always minimally visible when ScrollX is off and table gets too small. Not recommended if columns are resizable.
## ImGui_TableFlags_NoPadInnerX
```
integer reaper.ImGui_TableFlags_NoPadInnerX()
```

Disable inner padding between columns (double inner padding if TableFlags_BordersOuterV is on, single inner padding if BordersOuterV is off).
## ImGui_TableFlags_NoPadOuterX
```
integer reaper.ImGui_TableFlags_NoPadOuterX()
```

Default if TableFlags_BordersOuterV is off. Disable outermost padding.
## ImGui_TableFlags_NoSavedSettings
```
integer reaper.ImGui_TableFlags_NoSavedSettings()
```

Disable persisting columns order, width and sort settings in the .ini file.
## ImGui_TableFlags_None
```
integer reaper.ImGui_TableFlags_None()
```

No description available.
## ImGui_TableFlags_PadOuterX
```
integer reaper.ImGui_TableFlags_PadOuterX()
```

Default if TableFlags_BordersOuterV is on. Enable outermost padding. Generally desirable if you have headers.
## ImGui_TableFlags_PreciseWidths
```
integer reaper.ImGui_TableFlags_PreciseWidths()
```

Disable distributing remainder width to stretched columns (width allocation on a 100-wide table with 3 columns: Without this flag: 33,33,34. With this flag: 33,33,33). With larger number of columns, resizing will appear to be less smooth.
## ImGui_TableFlags_Reorderable
```
integer reaper.ImGui_TableFlags_Reorderable()
```

Enable reordering columns in header row (need calling TableSetupColumn + TableHeadersRow to display headers).
## ImGui_TableFlags_Resizable
```
integer reaper.ImGui_TableFlags_Resizable()
```

Enable resizing columns.
## ImGui_TableFlags_RowBg
```
integer reaper.ImGui_TableFlags_RowBg()
```

Set each RowBg color with Col_TableRowBg or Col_TableRowBgAlt (equivalent of calling TableSetBgColor with TableBgTarget_RowBg0 on each row manually).
## ImGui_TableFlags_ScrollX
```
integer reaper.ImGui_TableFlags_ScrollX()
```

Enable horizontal scrolling. Require 'outer_size' parameter of BeginTable to specify the container size. Changes default sizing policy. Because this creates a child window, ScrollY is currently generally recommended when using ScrollX.
## ImGui_TableFlags_ScrollY
```
integer reaper.ImGui_TableFlags_ScrollY()
```

Enable vertical scrolling. Require 'outer_size' parameter of BeginTable to specify the container size.
## ImGui_TableFlags_SizingFixedFit
```
integer reaper.ImGui_TableFlags_SizingFixedFit()
```

Columns default to _WidthFixed or _WidthAuto (if resizable or not resizable), matching contents width.
## ImGui_TableFlags_SizingFixedSame
```
integer reaper.ImGui_TableFlags_SizingFixedSame()
```

Columns default to _WidthFixed or _WidthAuto (if resizable or not resizable), matching the maximum contents width of all columns. Implicitly enable TableFlags_NoKeepColumnsVisible.
## ImGui_TableFlags_SizingStretchProp
```
integer reaper.ImGui_TableFlags_SizingStretchProp()
```

Columns default to _WidthStretch with default weights proportional to each columns contents widths.
## ImGui_TableFlags_SizingStretchSame
```
integer reaper.ImGui_TableFlags_SizingStretchSame()
```

Columns default to _WidthStretch with default weights all equal, unless overriden by TableSetupColumn.
## ImGui_TableFlags_SortMulti
```
integer reaper.ImGui_TableFlags_SortMulti()
```

Hold shift when clicking headers to sort on multiple column. TableGetColumnSortSpecs may return specs where (SpecsCount > 1).
## ImGui_TableFlags_SortTristate
```
integer reaper.ImGui_TableFlags_SortTristate()
```

Allow no sorting, disable default sorting. TableGetColumnSortSpecs may return specs where (SpecsCount == 0).
## ImGui_TableFlags_Sortable
```
integer reaper.ImGui_TableFlags_Sortable()
```

Enable sorting. Call TableNeedSort/TableGetColumnSortSpecs to obtain sort specs. Also see TableFlags_SortMulti and TableFlags_SortTristate.
## ImGui_TableGetColumnCount
```
integer reaper.ImGui_TableGetColumnCount(ImGui_Context ctx)
```

Return number of columns (value passed to BeginTable).
## ImGui_TableGetColumnFlags
```
integer reaper.ImGui_TableGetColumnFlags(ImGui_Context ctx, optional integer column_nIn)
```

Return column flags so you can query their Enabled/Visible/Sorted/Hovered
status flags. Pass -1 to use current column.
## ImGui_TableGetColumnIndex
```
integer reaper.ImGui_TableGetColumnIndex(ImGui_Context ctx)
```

Return current column index.
## ImGui_TableGetColumnName
```
string reaper.ImGui_TableGetColumnName(ImGui_Context ctx, optional integer column_nIn)
```

Return "" if column didn't have a name declared by TableSetupColumn.
Pass -1 to use current column.
## ImGui_TableGetColumnSortSpecs
```
boolean retval, integer column_index, integer column_user_id, integer sort_direction = reaper.ImGui_TableGetColumnSortSpecs(ImGui_Context ctx, integer id)
```

Sorting specification for one column of a table.
Call while incrementing 'id' from 0 until false is returned.
## ImGui_TableGetHoveredColumn
```
integer reaper.ImGui_TableGetHoveredColumn(ImGui_Context ctx)
```

Returns hovered column or -1 when table is not hovered. Returns columns_count
if the unused space at the right of visible columns is hovered.
## ImGui_TableGetRowIndex
```
integer reaper.ImGui_TableGetRowIndex(ImGui_Context ctx)
```

Return current row index.
## ImGui_TableHeader
```
reaper.ImGui_TableHeader(ImGui_Context ctx, string label)
```

Submit one header cell manually (rarely used). See TableSetupColumn.
## ImGui_TableHeadersRow
```
reaper.ImGui_TableHeadersRow(ImGui_Context ctx)
```

Submit a row with headers cells based on data provided to TableSetupColumn
+ submit context menu.
## ImGui_TableNeedSort
```
boolean retval, boolean has_specs = reaper.ImGui_TableNeedSort(ImGui_Context ctx)
```

Return true once when sorting specs have changed since last call,
or the first time. 'has_specs' is false when not sorting.
## ImGui_TableNextColumn
```
boolean reaper.ImGui_TableNextColumn(ImGui_Context ctx)
```

Append into the next column (or first column of next row if currently in
last column). Return true when column is visible.
## ImGui_TableNextRow
```
reaper.ImGui_TableNextRow(ImGui_Context ctx, optional integer row_flagsIn, optional number min_row_heightIn)
```

Append into the first cell of a new row.
## ImGui_TableRowFlags_Headers
```
integer reaper.ImGui_TableRowFlags_Headers()
```

Identify header row (set default background color + width of its contents accounted different for auto column width).
## ImGui_TableRowFlags_None
```
integer reaper.ImGui_TableRowFlags_None()
```

For TableNextRow.
## ImGui_TableSetBgColor
```
reaper.ImGui_TableSetBgColor(ImGui_Context ctx, integer target, integer color_rgba, optional integer column_nIn)
```

Change the color of a cell, row, or column.
See TableBgTarget_* flags for details.
## ImGui_TableSetColumnEnabled
```
reaper.ImGui_TableSetColumnEnabled(ImGui_Context ctx, integer column_n, boolean v)
```

Change user-accessible enabled/disabled state of a column, set to false to
hide the column. Note that end-user can use the context menu to change this
themselves (right-click in headers, or right-click in columns body with
TableFlags_ContextMenuInBody).
## ImGui_TableSetColumnIndex
```
boolean reaper.ImGui_TableSetColumnIndex(ImGui_Context ctx, integer column_n)
```

Append into the specified column. Return true when column is visible.
## ImGui_TableSetupColumn
```
reaper.ImGui_TableSetupColumn(ImGui_Context ctx, string label, optional integer flagsIn, optional number init_width_or_weightIn, optional integer user_idIn)
```

Use to specify label, resizing policy, default width/weight, id,
various other flags etc.
## ImGui_TableSetupScrollFreeze
```
reaper.ImGui_TableSetupScrollFreeze(ImGui_Context ctx, integer cols, integer rows)
```

Lock columns/rows so they stay visible when scrolled.
## ImGui_Text
```
reaper.ImGui_Text(ImGui_Context ctx, string text)
```

No description available.
## ImGui_TextColored
```
reaper.ImGui_TextColored(ImGui_Context ctx, integer col_rgba, string text)
```

Shortcut for PushStyleColor(Col_Text, color); Text(text); PopStyleColor();
## ImGui_TextDisabled
```
reaper.ImGui_TextDisabled(ImGui_Context ctx, string text)
```

No description available.
## ImGui_TextFilter_Clear
```
reaper.ImGui_TextFilter_Clear(ImGui_TextFilter filter)
```

No description available.
## ImGui_TextFilter_Draw
```
boolean reaper.ImGui_TextFilter_Draw(ImGui_TextFilter filter, ImGui_Context ctx, optional string labelIn, optional number widthIn)
```

Helper calling InputText+TextFilter_Set
## ImGui_TextFilter_Get
```
string reaper.ImGui_TextFilter_Get(ImGui_TextFilter filter)
```

No description available.
## ImGui_TextFilter_IsActive
```
boolean reaper.ImGui_TextFilter_IsActive(ImGui_TextFilter filter)
```

No description available.
## ImGui_TextFilter_PassFilter
```
boolean reaper.ImGui_TextFilter_PassFilter(ImGui_TextFilter filter, string text)
```

No description available.
## ImGui_TextFilter_Set
```
reaper.ImGui_TextFilter_Set(ImGui_TextFilter filter, string filter_text)
```

No description available.
## ImGui_TextWrapped
```
reaper.ImGui_TextWrapped(ImGui_Context ctx, string text)
```

Shortcut for PushTextWrapPos(0.0); Text(text); PopTextWrapPos();.
Note that this won't work on an auto-resizing window if there's no other
widgets to extend the window width, yoy may need to set a size using
SetNextWindowSize.
## ImGui_TreeNode
```
boolean reaper.ImGui_TreeNode(ImGui_Context ctx, string label, optional integer flagsIn)
```

TreeNode functions return true when the node is open, in which case you need
to also call TreePop when you are finished displaying the tree node contents.
## ImGui_TreeNodeEx
```
boolean reaper.ImGui_TreeNodeEx(ImGui_Context ctx, string str_id, string label, optional integer flagsIn)
```

Helper variation to easily decorelate the id from the displayed string.
Read the [FAQ](https://dearimgui.com/faq) about why and how to use ID.
To align arbitrary text at the same level as a TreeNode you can use Bullet.
## ImGui_TreeNodeFlags_AllowOverlap
```
integer reaper.ImGui_TreeNodeFlags_AllowOverlap()
```

Hit testing to allow subsequent widgets to overlap this one.
## ImGui_TreeNodeFlags_Bullet
```
integer reaper.ImGui_TreeNodeFlags_Bullet()
```

Display a bullet instead of arrow. IMPORTANT: node can still be marked open/close if you don't set the _Leaf flag!
## ImGui_TreeNodeFlags_CollapsingHeader
```
integer reaper.ImGui_TreeNodeFlags_CollapsingHeader()
```

TreeNodeFlags_Framed | TreeNodeFlags_NoTreePushOnOpen | TreeNodeFlags_NoAutoOpenOnLog
## ImGui_TreeNodeFlags_DefaultOpen
```
integer reaper.ImGui_TreeNodeFlags_DefaultOpen()
```

Default node to be open.
## ImGui_TreeNodeFlags_FramePadding
```
integer reaper.ImGui_TreeNodeFlags_FramePadding()
```

Use FramePadding (even for an unframed text node) to vertically align text baseline to regular widget height. Equivalent to calling AlignTextToFramePadding before the node.
## ImGui_TreeNodeFlags_Framed
```
integer reaper.ImGui_TreeNodeFlags_Framed()
```

Draw frame with background (e.g. for CollapsingHeader).
## ImGui_TreeNodeFlags_Leaf
```
integer reaper.ImGui_TreeNodeFlags_Leaf()
```

No collapsing, no arrow (use as a convenience for leaf nodes).
## ImGui_TreeNodeFlags_NoAutoOpenOnLog
```
integer reaper.ImGui_TreeNodeFlags_NoAutoOpenOnLog()
```

Don't automatically and temporarily open node when Logging is active (by default logging will automatically open tree nodes).
## ImGui_TreeNodeFlags_NoTreePushOnOpen
```
integer reaper.ImGui_TreeNodeFlags_NoTreePushOnOpen()
```

Don't do a TreePush when open (e.g. for CollapsingHeader) = no extra indent nor pushing on ID stack.
## ImGui_TreeNodeFlags_None
```
integer reaper.ImGui_TreeNodeFlags_None()
```

No description available.
## ImGui_TreeNodeFlags_OpenOnArrow
```
integer reaper.ImGui_TreeNodeFlags_OpenOnArrow()
```

Only open when clicking on the arrow part. If TreeNodeFlags_OpenOnDoubleClick is also set, single-click arrow or double-click all box to open.
## ImGui_TreeNodeFlags_OpenOnDoubleClick
```
integer reaper.ImGui_TreeNodeFlags_OpenOnDoubleClick()
```

Need double-click to open node.
## ImGui_TreeNodeFlags_Selected
```
integer reaper.ImGui_TreeNodeFlags_Selected()
```

Draw as selected.
## ImGui_TreeNodeFlags_SpanAllColumns
```
integer reaper.ImGui_TreeNodeFlags_SpanAllColumns()
```

Frame will span all columns of its container table (text will still fit in current column).
## ImGui_TreeNodeFlags_SpanAvailWidth
```
integer reaper.ImGui_TreeNodeFlags_SpanAvailWidth()
```

Extend hit box to the right-most edge, even if not framed. This is not the default in order to allow adding other items on the same line. In the future we may refactor the hit system to be front-to-back, allowing natural overlaps and then this can become the default.
## ImGui_TreeNodeFlags_SpanFullWidth
```
integer reaper.ImGui_TreeNodeFlags_SpanFullWidth()
```

Extend hit box to the left-most and right-most edges (bypass the indented area).
## ImGui_TreeNodeFlags_SpanTextWidth
```
integer reaper.ImGui_TreeNodeFlags_SpanTextWidth()
```

Narrow hit box + narrow hovering highlight, will only cover the label text.
## ImGui_TreePop
```
reaper.ImGui_TreePop(ImGui_Context ctx)
```

Unindent()+PopID()
## ImGui_TreePush
```
reaper.ImGui_TreePush(ImGui_Context ctx, string str_id)
```

Indent()+PushID(). Already called by TreeNode when returning true,
but you can call TreePush/TreePop yourself if desired.
## ImGui_Unindent
```
reaper.ImGui_Unindent(ImGui_Context ctx, optional number indent_wIn)
```

Move content position back to the left, by 'indent_w', or
StyleVar_IndentSpacing if 'indent_w' <= 0
## ImGui_VSliderDouble
```
boolean retval, number v = reaper.ImGui_VSliderDouble(ImGui_Context ctx, string label, number size_w, number size_h, number v, number v_min, number v_max, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_VSliderInt
```
boolean retval, integer v = reaper.ImGui_VSliderInt(ImGui_Context ctx, string label, number size_w, number size_h, integer v, integer v_min, integer v_max, optional string formatIn, optional integer flagsIn)
```

No description available.
## ImGui_ValidatePtr
```
boolean reaper.ImGui_ValidatePtr(identifier pointer, string type)
```

Return whether the given pointer is a valid instance of one of the following
types (indentation represents inheritance):
## ImGui_Viewport_GetCenter
```
number x, number y = reaper.ImGui_Viewport_GetCenter(ImGui_Viewport viewport)
```

Center of the viewport.
## ImGui_Viewport_GetPos
```
number x, number y = reaper.ImGui_Viewport_GetPos(ImGui_Viewport viewport)
```

Main Area: Position of the viewport
## ImGui_Viewport_GetSize
```
number w, number h = reaper.ImGui_Viewport_GetSize(ImGui_Viewport viewport)
```

Main Area: Size of the viewport.
## ImGui_Viewport_GetWorkCenter
```
number x, number y = reaper.ImGui_Viewport_GetWorkCenter(ImGui_Viewport viewport)
```

Center of the viewport's work area.
## ImGui_Viewport_GetWorkPos
```
number x, number y = reaper.ImGui_Viewport_GetWorkPos(ImGui_Viewport viewport)
```

>= Viewport_GetPos
## ImGui_Viewport_GetWorkSize
```
number w, number h = reaper.ImGui_Viewport_GetWorkSize(ImGui_Viewport viewport)
```

<= Viewport_GetSize
## ImGui_WindowFlags_AlwaysAutoResize
```
integer reaper.ImGui_WindowFlags_AlwaysAutoResize()
```

Resize every window to its content every frame.
## ImGui_WindowFlags_AlwaysHorizontalScrollbar
```
integer reaper.ImGui_WindowFlags_AlwaysHorizontalScrollbar()
```

Always show horizontal scrollbar (even if ContentSize.x < Size.x).
## ImGui_WindowFlags_AlwaysVerticalScrollbar
```
integer reaper.ImGui_WindowFlags_AlwaysVerticalScrollbar()
```

Always show vertical scrollbar (even if ContentSize.y < Size.y).
## ImGui_WindowFlags_HorizontalScrollbar
```
integer reaper.ImGui_WindowFlags_HorizontalScrollbar()
```

Allow horizontal scrollbar to appear (off by default). You may use SetNextWindowContentSize(width, 0.0) prior to calling Begin() to specify width. Read code in the demo's "Horizontal Scrolling" section.
## ImGui_WindowFlags_MenuBar
```
integer reaper.ImGui_WindowFlags_MenuBar()
```

Has a menu-bar.
## ImGui_WindowFlags_NoBackground
```
integer reaper.ImGui_WindowFlags_NoBackground()
```

Disable drawing background color (WindowBg, etc.) and outside border. Similar as using SetNextWindowBgAlpha(0.0).
## ImGui_WindowFlags_NoCollapse
```
integer reaper.ImGui_WindowFlags_NoCollapse()
```

Disable user collapsing window by double-clicking on it. Also referred to as Window Menu Button (e.g. within a docking node).
## ImGui_WindowFlags_NoDecoration
```
integer reaper.ImGui_WindowFlags_NoDecoration()
```

WindowFlags_NoTitleBar | WindowFlags_NoResize | WindowFlags_NoScrollbar | WindowFlags_NoCollapse
## ImGui_WindowFlags_NoDocking
```
integer reaper.ImGui_WindowFlags_NoDocking()
```

Disable docking of this window.
## ImGui_WindowFlags_NoFocusOnAppearing
```
integer reaper.ImGui_WindowFlags_NoFocusOnAppearing()
```

Disable taking focus when transitioning from hidden to visible state.
## ImGui_WindowFlags_NoInputs
```
integer reaper.ImGui_WindowFlags_NoInputs()
```

WindowFlags_NoMouseInputs | WindowFlags_NoNavInputs | WindowFlags_NoNavFocus
## ImGui_WindowFlags_NoMouseInputs
```
integer reaper.ImGui_WindowFlags_NoMouseInputs()
```

Disable catching mouse, hovering test with pass through.
## ImGui_WindowFlags_NoMove
```
integer reaper.ImGui_WindowFlags_NoMove()
```

Disable user moving the window.
## ImGui_WindowFlags_NoNav
```
integer reaper.ImGui_WindowFlags_NoNav()
```

WindowFlags_NoNavInputs | WindowFlags_NoNavFocus
## ImGui_WindowFlags_NoNavFocus
```
integer reaper.ImGui_WindowFlags_NoNavFocus()
```

No focusing toward this window with gamepad/keyboard navigation (e.g. skipped by CTRL+TAB).
## ImGui_WindowFlags_NoNavInputs
```
integer reaper.ImGui_WindowFlags_NoNavInputs()
```

No gamepad/keyboard navigation within the window.
## ImGui_WindowFlags_NoResize
```
integer reaper.ImGui_WindowFlags_NoResize()
```

Disable user resizing with the lower-right grip.
## ImGui_WindowFlags_NoSavedSettings
```
integer reaper.ImGui_WindowFlags_NoSavedSettings()
```

Never load/save settings in .ini file.
## ImGui_WindowFlags_NoScrollWithMouse
```
integer reaper.ImGui_WindowFlags_NoScrollWithMouse()
```

Disable user vertically scrolling with mouse wheel. On child window, mouse wheel will be forwarded to the parent unless NoScrollbar is also set.
## ImGui_WindowFlags_NoScrollbar
```
integer reaper.ImGui_WindowFlags_NoScrollbar()
```

Disable scrollbars (window can still scroll with mouse or programmatically).
## ImGui_WindowFlags_NoTitleBar
```
integer reaper.ImGui_WindowFlags_NoTitleBar()
```

Disable title-bar.
## ImGui_WindowFlags_None
```
integer reaper.ImGui_WindowFlags_None()
```

Default flag.
## ImGui_WindowFlags_TopMost
```
integer reaper.ImGui_WindowFlags_TopMost()
```

Show the window above all non-topmost windows.
## ImGui_WindowFlags_UnsavedDocument
```
integer reaper.ImGui_WindowFlags_UnsavedDocument()
```

Display a dot next to the title. When used in a tab/docking context, tab is selected when clicking the X + closure is not assumed (will wait for user to stop submitting the tab). Otherwise closure is assumed when pressing the X, so if you keep submitting the tab may reappear at end of tab bar.
## ImGui__getapi
```
identifier reaper.ImGui__getapi(string version, string symbol_name)
```

Internal use only.
## ImGui__geterr
```
string reaper.ImGui__geterr()
```

Internal use only.
## ImGui__init
```
string buf = reaper.ImGui__init(string buf)
```

Internal use only.
## ImGui__setshim
```
reaper.ImGui__setshim(string version, string symbol_name)
```

Internal use only.
## ImGui__shim
```
reaper.ImGui__shim()
```

Internal use only.
## JB_GetSWSExtraProjectNotes
```
string reaper.JB_GetSWSExtraProjectNotes(ReaProject project)
```

No description available.
## JB_SetSWSExtraProjectNotes
```
reaper.JB_SetSWSExtraProjectNotes(ReaProject project, string str)
```

No description available.
## JS_Actions_CountShortcuts
```
integer reaper.JS_Actions_CountShortcuts(integer section, integer cmdID)
```

Section:
0 = Main, 100 = Main (alt recording), 32060 = MIDI Editor, 32061 = MIDI Event List Editor, 32062 = MIDI Inline Editor, 32063 = Media Explorer.
## JS_Actions_DeleteShortcut
```
boolean reaper.JS_Actions_DeleteShortcut(integer section, integer cmdID, integer shortcutidx)
```

Section:
0 = Main, 100 = Main (alt recording), 32060 = MIDI Editor, 32061 = MIDI Event List Editor, 32062 = MIDI Inline Editor, 32063 = Media Explorer.
## JS_Actions_DoShortcutDialog
```
boolean reaper.JS_Actions_DoShortcutDialog(integer section, integer cmdID, integer shortcutidx)
```

Section:
0 = Main, 100 = Main (alt recording), 32060 = MIDI Editor, 32061 = MIDI Event List Editor, 32062 = MIDI Inline Editor, 32063 = Media Explorer.
## JS_Actions_GetShortcutDesc
```
boolean retval, string desc = reaper.JS_Actions_GetShortcutDesc(integer section, integer cmdID, integer shortcutidx)
```

Section:
0 = Main, 100 = Main (alt recording), 32060 = MIDI Editor, 32061 = MIDI Event List Editor, 32062 = MIDI Inline Editor, 32063 = Media Explorer.
## JS_Byte
```
integer byte = reaper.JS_Byte(identifier pointer, integer offset)
```

Returns the unsigned byte at address[offset]. Offset is added as steps of 1 byte each.
## JS_Composite
```
integer reaper.JS_Composite(identifier windowHWND, integer dstx, integer dsty, integer dstw, integer dsth, identifier sysBitmap, integer srcx, integer srcy, integer srcw, integer srch, unsupported autoUpdate)
```

Composites a LICE bitmap with a REAPER window. Each time that the window is re-drawn, the bitmap will be blitted over the window's client area (with per-pixel alpha blending).
## JS_Composite_Delay
```
integer retval, number prevMinTime, number prevMaxTime, integer prevBitmaps = reaper.JS_Composite_Delay(identifier windowHWND, number minTime, number maxTime, integer numBitmapsWhenMax)
```

On WindowsOS, flickering of composited images can be improved considerably by slowing the refresh rate of the window. The optimal refresh rate may depend on the number of composited bitmaps.
## JS_Composite_ListBitmaps
```
integer retval, string list = reaper.JS_Composite_ListBitmaps(identifier windowHWND)
```

Returns all bitmaps composited to the given window.
## JS_Composite_Unlink
```
reaper.JS_Composite_Unlink(identifier windowHWND, identifier bitmap, unsupported autoUpdate)
```

Unlinks the window and bitmap.
## JS_Dialog_BrowseForFolder
```
integer retval, string folder = reaper.JS_Dialog_BrowseForFolder(string caption, string initialFolder)
```

retval is 1 if a file was selected, 0 if the user cancelled the dialog, and -1 if an error occurred.
## JS_Dialog_BrowseForOpenFiles
```
integer retval, string fileNames = reaper.JS_Dialog_BrowseForOpenFiles(string windowTitle, string initialFolder, string initialFile, string extensionList, boolean allowMultiple)
```

If allowMultiple is true, multiple files may be selected. The returned string is \0-separated, with the first substring containing the folder path and subsequent substrings containing the file names. * On macOS, the first substring may be empty, and each file name will then contain its entire path. * This function only allows selection of existing files, and does not allow creation of new files.
## JS_Dialog_BrowseForSaveFile
```
integer retval, string fileName = reaper.JS_Dialog_BrowseForSaveFile(string windowTitle, string initialFolder, string initialFile, string extensionList)
```

retval is 1 if a file was selected, 0 if the user cancelled the dialog, or negative if an error occurred.
## JS_Double
```
number double = reaper.JS_Double(identifier pointer, integer offset)
```

Returns the 8-byte floating point value at address[offset]. Offset is added as steps of 8 bytes each.
## JS_File_Stat
```
integer retval, number size, string accessedTime, string modifiedTime, string cTime, integer deviceID, integer deviceSpecialID, integer inode, integer mode, integer numLinks, integer ownerUserID, integer ownerGroupID = reaper.JS_File_Stat(string filePath)
```

Returns information about a file.
## JS_GDI_Blit
```
reaper.JS_GDI_Blit(identifier destHDC, integer dstx, integer dsty, identifier sourceHDC, integer srcx, integer srxy, integer width, integer height, optional string mode)
```

Blits between two device contexts, which may include LICE "system bitmaps".
## JS_GDI_CreateFillBrush
```
identifier reaper.JS_GDI_CreateFillBrush(integer color)
```

No description available.
## JS_GDI_CreateFont
```
identifier reaper.JS_GDI_CreateFont(integer height, integer weight, integer angle, boolean italic, boolean underline, boolean strike, string fontName)
```

Parameters: * weight: 0 - 1000, with 0 = auto, 400 = normal and 700 = bold. * angle: the angle, in tenths of degrees, between the text and the x-axis of the device. * fontName: If empty string "", uses first font that matches the other specified attributes.
## JS_GDI_CreatePen
```
identifier reaper.JS_GDI_CreatePen(integer width, integer color)
```

No description available.
## JS_GDI_DeleteObject
```
reaper.JS_GDI_DeleteObject(identifier GDIObject)
```

No description available.
## JS_GDI_DrawText
```
integer reaper.JS_GDI_DrawText(identifier deviceHDC, string text, integer len, integer left, integer top, integer right, integer bottom, string align))
```

Parameters: * align: Combination of: "TOP", "VCENTER", "LEFT", "HCENTER", "RIGHT", "BOTTOM", "WORDBREAK", "SINGLELINE", "NOCLIP", "CALCRECT", "NOPREFIX" or "ELLIPSIS"
## JS_GDI_FillEllipse
```
reaper.JS_GDI_FillEllipse(identifier deviceHDC, integer left, integer top, integer right, integer bottom)
```

No description available.
## JS_GDI_FillPolygon
```
reaper.JS_GDI_FillPolygon(identifier deviceHDC, string packedX, string packedY, integer numPoints)
```

packedX and packedY are strings of points, each packed as "<i4".
## JS_GDI_FillRect
```
reaper.JS_GDI_FillRect(identifier deviceHDC, integer left, integer top, integer right, integer bottom)
```

No description available.
## JS_GDI_FillRoundRect
```
reaper.JS_GDI_FillRoundRect(identifier deviceHDC, integer left, integer top, integer right, integer bottom, integer xrnd, integer yrnd)
```

No description available.
## JS_GDI_GetClientDC
```
identifier reaper.JS_GDI_GetClientDC(identifier windowHWND)
```

Returns the device context for the client area of the specified window.
## JS_GDI_GetScreenDC
```
identifier reaper.JS_GDI_GetScreenDC()
```

Returns a device context for the entire screen.
## JS_GDI_GetSysColor
```
integer reaper.JS_GDI_GetSysColor(string GUIElement)
```

No description available.
## JS_GDI_GetTextColor
```
integer reaper.JS_GDI_GetTextColor(identifier deviceHDC)
```

No description available.
## JS_GDI_GetWindowDC
```
identifier reaper.JS_GDI_GetWindowDC(identifier windowHWND)
```

Returns the device context for the entire window, including title bar and frame.
## JS_GDI_Line
```
reaper.JS_GDI_Line(identifier deviceHDC, integer x1, integer y1, integer x2, integer y2)
```

No description available.
## JS_GDI_Polyline
```
reaper.JS_GDI_Polyline(identifier deviceHDC, string packedX, string packedY, integer numPoints)
```

packedX and packedY are strings of points, each packed as "<i4".
## JS_GDI_ReleaseDC
```
integer reaper.JS_GDI_ReleaseDC(identifier deviceHDC, identifier windowHWND)
```

To release a window HDC, both arguments must be supplied: the HWND as well as the HDC. To release a screen DC, only the HDC needs to be supplied.
## JS_GDI_SelectObject
```
identifier reaper.JS_GDI_SelectObject(identifier deviceHDC, identifier GDIObject)
```

Activates a font, pen, or fill brush for subsequent drawing in the specified device context.
## JS_GDI_SetPixel
```
reaper.JS_GDI_SetPixel(identifier deviceHDC, integer x, integer y, integer color)
```

No description available.
## JS_GDI_SetTextBkColor
```
reaper.JS_GDI_SetTextBkColor(identifier deviceHDC, integer color)
```

No description available.
## JS_GDI_SetTextBkMode
```
reaper.JS_GDI_SetTextBkMode(identifier deviceHDC, integer mode)
```

No description available.
## JS_GDI_SetTextColor
```
reaper.JS_GDI_SetTextColor(identifier deviceHDC, integer color)
```

No description available.
## JS_GDI_StretchBlit
```
reaper.JS_GDI_StretchBlit(identifier destHDC, integer dstx, integer dsty, integer dstw, integer dsth, identifier sourceHDC, integer srcx, integer srxy, integer srcw, integer srch, optional string mode)
```

Blits between two device contexts, which may include LICE "system bitmaps".
## JS_Header_GetItemCount
```
integer reaper.JS_Header_GetItemCount(identifier headerHWND)
```

No description available.
## JS_Int
```
integer int = reaper.JS_Int(identifier pointer, integer offset)
```

Returns the 4-byte signed integer at address[offset]. Offset is added as steps of 4 bytes each.
## JS_LICE_AlterBitmapHSV
```
reaper.JS_LICE_AlterBitmapHSV(identifier bitmap, number hue, number saturation, number value)
```

Hue is rolled over, saturation and value are clamped, all 0..1. (Alpha remains unchanged.)
## JS_LICE_AlterRectHSV
```
reaper.JS_LICE_AlterRectHSV(identifier bitmap, integer x, integer y, integer w, integer h, number hue, number saturation, number value)
```

Hue is rolled over, saturation and value are clamped, all 0..1. (Alpha remains unchanged.)
## JS_LICE_Arc
```
reaper.JS_LICE_Arc(identifier bitmap, number cx, number cy, number r, number minAngle, number maxAngle, integer color, number alpha, string mode, boolean antialias)
```

LICE modes: "COPY" (default if empty string), "MASK", "ADD", "DODGE", "MUL", "OVERLAY" or "HSVADJ", any of which may be combined with "ALPHA".
## JS_LICE_ArrayAllBitmaps
```
integer reaper.JS_LICE_ArrayAllBitmaps(identifier reaperarray)
```

No description available.
## JS_LICE_Bezier
```
reaper.JS_LICE_Bezier(identifier bitmap, number xstart, number ystart, number xctl1, number yctl1, number xctl2, number yctl2, number xend, number yend, number tol, integer color, number alpha, string mode, boolean antialias)
```

LICE modes: "COPY" (default if empty string), "MASK", "ADD", "DODGE", "MUL", "OVERLAY" or "HSVADJ", any of which may be combined with "ALPHA" to enable per-pixel alpha blending.
## JS_LICE_Blit
```
reaper.JS_LICE_Blit(identifier destBitmap, integer dstx, integer dsty, identifier sourceBitmap, integer srcx, integer srcy, integer width, integer height, number alpha, string mode)
```

Standard LICE modes: "COPY" (default if empty string), "MASK", "ADD", "DODGE", "MUL", "OVERLAY" or "HSVADJ", any of which may be combined with "ALPHA" to enable per-pixel alpha blending.
## JS_LICE_Circle
```
reaper.JS_LICE_Circle(identifier bitmap, number cx, number cy, number r, integer color, number alpha, string mode, boolean antialias)
```

LICE modes: "COPY" (default if empty string), "MASK", "ADD", "DODGE", "MUL", "OVERLAY" or "HSVADJ", any of which may be combined with "ALPHA".
## JS_LICE_Clear
```
reaper.JS_LICE_Clear(identifier bitmap, integer color)
```

No description available.
## JS_LICE_CreateBitmap
```
identifier reaper.JS_LICE_CreateBitmap(boolean isSysBitmap, integer width, integer height)
```

No description available.
## JS_LICE_CreateFont
```
identifier reaper.JS_LICE_CreateFont()
```

No description available.
## JS_LICE_DestroyBitmap
```
reaper.JS_LICE_DestroyBitmap(identifier bitmap)
```

Deletes the bitmap, and also unlinks bitmap from any composited window.
## JS_LICE_DestroyFont
```
reaper.JS_LICE_DestroyFont(identifier LICEFont)
```

No description available.
## JS_LICE_DrawChar
```
reaper.JS_LICE_DrawChar(identifier bitmap, integer x, integer y, integer c, integer color, number alpha, integer mode))
```

No description available.
## JS_LICE_DrawText
```
integer reaper.JS_LICE_DrawText(identifier bitmap, identifier LICEFont, string text, integer textLen, integer x1, integer y1, integer x2, integer y2)
```

No description available.
## JS_LICE_FillCircle
```
reaper.JS_LICE_FillCircle(identifier bitmap, number cx, number cy, number r, integer color, number alpha, string mode, boolean antialias)
```

LICE modes: "COPY" (default if empty string), "MASK", "ADD", "DODGE", "MUL", "OVERLAY" or "HSVADJ", any of which may be combined with "ALPHA".
## JS_LICE_FillPolygon
```
reaper.JS_LICE_FillPolygon(identifier bitmap, string packedX, string packedY, integer numPoints, integer color, number alpha, string mode)
```

packedX and packedY are two strings of coordinates, each packed as "<i4".
## JS_LICE_FillRect
```
reaper.JS_LICE_FillRect(identifier bitmap, integer x, integer y, integer w, integer h, integer color, number alpha, string mode)
```

LICE modes: "COPY" (default if empty string), "MASK", "ADD", "DODGE", "MUL", "OVERLAY" or "HSVADJ", any of which may be combined with "ALPHA".
## JS_LICE_FillTriangle
```
reaper.JS_LICE_FillTriangle(identifier bitmap, integer x1, integer y1, integer x2, integer y2, integer x3, integer y3, integer color, number alpha, string mode)
```

LICE modes: "COPY" (default if empty string), "MASK", "ADD", "DODGE", "MUL", "OVERLAY" or "HSVADJ", any of which may be combined with "ALPHA".
## JS_LICE_GetDC
```
identifier reaper.JS_LICE_GetDC(identifier bitmap)
```

No description available.
## JS_LICE_GetHeight
```
integer reaper.JS_LICE_GetHeight(identifier bitmap)
```

No description available.
## JS_LICE_GetPixel
```
number color = reaper.JS_LICE_GetPixel(identifier bitmap, integer x, integer y)
```

Returns the color of the specified pixel.
## JS_LICE_GetWidth
```
integer reaper.JS_LICE_GetWidth(identifier bitmap)
```

No description available.
## JS_LICE_GradRect
```
reaper.JS_LICE_GradRect(identifier bitmap, integer dstx, integer dsty, integer dstw, integer dsth, number ir, number ig, number ib, number ia, number drdx, number dgdx, number dbdx, number dadx, number drdy, number dgdy, number dbdy, number dady, string mode)
```

No description available.
## JS_LICE_IsFlipped
```
boolean reaper.JS_LICE_IsFlipped(identifier bitmap)
```

No description available.
## JS_LICE_Line
```
reaper.JS_LICE_Line(identifier bitmap, number x1, number y1, number x2, number y2, integer color, number alpha, string mode, boolean antialias)
```

LICE modes: "COPY" (default if empty string), "MASK", "ADD", "DODGE", "MUL", "OVERLAY" or "HSVADJ", any of which may be combined with "ALPHA".
## JS_LICE_ListAllBitmaps
```
integer retval, string list = reaper.JS_LICE_ListAllBitmaps()
```

No description available.
## JS_LICE_LoadJPG
```
identifier reaper.JS_LICE_LoadJPG(string filename)
```

Returns a system LICE bitmap containing the JPEG.
## JS_LICE_LoadJPGFromMemory
```
identifier reaper.JS_LICE_LoadJPGFromMemory(string buffer, integer bufsize)
```

Returns a system LICE bitmap containing the JPEG.
## JS_LICE_LoadPNG
```
identifier reaper.JS_LICE_LoadPNG(string filename)
```

Returns a system LICE bitmap containing the PNG.
## JS_LICE_LoadPNGFromMemory
```
identifier reaper.JS_LICE_LoadPNGFromMemory(string buffer, integer bufsize)
```

Returns a system LICE bitmap containing the PNG.
## JS_LICE_MeasureText
```
integer width, integer Height = reaper.JS_LICE_MeasureText(string text)
```

No description available.
## JS_LICE_ProcessRect
```
boolean reaper.JS_LICE_ProcessRect(identifier bitmap, integer x, integer y, integer w, integer h, string mode, number operand)
```

Applies bitwise operations to each pixel in the target rectangle.
## JS_LICE_PutPixel
```
reaper.JS_LICE_PutPixel(identifier bitmap, integer x, integer y, number color, number alpha, string mode)
```

LICE modes: "COPY" (default if empty string), "MASK", "ADD", "DODGE", "MUL", "OVERLAY" or "HSVADJ", any of which may be combined with "ALPHA".
## JS_LICE_Resize
```
reaper.JS_LICE_Resize(identifier bitmap, integer width, integer height)
```

No description available.
## JS_LICE_RotatedBlit
```
reaper.JS_LICE_RotatedBlit(identifier destBitmap, integer dstx, integer dsty, integer dstw, integer dsth, identifier sourceBitmap, number srcx, number srcy, number srcw, number srch, number angle, number rotxcent, number rotycent, boolean cliptosourcerect, number alpha, string mode)
```

LICE modes: "COPY" (default if empty string), "MASK", "ADD", "DODGE", "MUL", "OVERLAY" or "HSVADJ", any of which may be combined with "ALPHA" to enable per-pixel alpha blending.
## JS_LICE_RoundRect
```
reaper.JS_LICE_RoundRect(identifier bitmap, number x, number y, number w, number h, integer cornerradius, integer color, number alpha, string mode, boolean antialias)
```

LICE modes: "COPY" (default if empty string), "MASK", "ADD", "DODGE", "MUL", "OVERLAY" or "HSVADJ", any of which may be combined with "ALPHA".
## JS_LICE_ScaledBlit
```
reaper.JS_LICE_ScaledBlit(identifier destBitmap, integer dstx, integer dsty, integer dstw, integer dsth, identifier srcBitmap, number srcx, number srcy, number srcw, number srch, number alpha, string mode)
```

LICE modes: "COPY" (default if empty string), "MASK", "ADD", "DODGE", "MUL", "OVERLAY" or "HSVADJ", any of which may be combined with "ALPHA" to enable per-pixel alpha blending.
## JS_LICE_SetAlphaFromColorMask
```
reaper.JS_LICE_SetAlphaFromColorMask(identifier bitmap, integer colorRGB)
```

Sets all pixels that match the given color's RGB values to fully transparent, and all other pixels to fully opaque. (All pixels' RGB values remain unchanged.)
## JS_LICE_SetFontBkColor
```
reaper.JS_LICE_SetFontBkColor(identifier LICEFont, integer color)
```

Sets the color of the font background.
## JS_LICE_SetFontColor
```
reaper.JS_LICE_SetFontColor(identifier LICEFont, integer color)
```

No description available.
## JS_LICE_SetFontFXColor
```
reaper.JS_LICE_SetFontFXColor(identifier LICEFont, integer color)
```

Sets the color of font FX such as shadow.
## JS_LICE_SetFontFromGDI
```
reaper.JS_LICE_SetFontFromGDI(identifier LICEFont, identifier GDIFont, string moreFormats)
```

Converts a GDI font into a LICE font.
## JS_LICE_WriteJPG
```
boolean reaper.JS_LICE_WriteJPG(string filename, identifier bitmap, integer quality, unsupported forceBaseline)
```

Parameters:
## JS_LICE_WritePNG
```
boolean reaper.JS_LICE_WritePNG(string filename, identifier bitmap, boolean wantAlpha)
```

No description available.
## JS_ListView_EnsureVisible
```
reaper.JS_ListView_EnsureVisible(identifier listviewHWND, integer index, boolean partialOK)
```

No description available.
## JS_ListView_EnumSelItems
```
integer reaper.JS_ListView_EnumSelItems(identifier listviewHWND, integer index)
```

Returns the index of the next selected list item with index greater that the specified number. Returns -1 if no selected items left.
## JS_ListView_GetFocusedItem
```
integer retval, string text = reaper.JS_ListView_GetFocusedItem(identifier listviewHWND)
```

Returns the index and text of the focused item, if any.
## JS_ListView_GetHeader
```
identifier reaper.JS_ListView_GetHeader(identifier listviewHWND)
```

No description available.
## JS_ListView_GetItem
```
string text, integer state = reaper.JS_ListView_GetItem(identifier listviewHWND, integer index, integer subItem)
```

Returns the text and state of specified item.
## JS_ListView_GetItemCount
```
integer reaper.JS_ListView_GetItemCount(identifier listviewHWND)
```

No description available.
## JS_ListView_GetItemRect
```
boolean retval, integer left, integer top, integer right, integer bottom = reaper.JS_ListView_GetItemRect(identifier listviewHWND, integer index)
```

Returns client coordinates of the item.
## JS_ListView_GetItemState
```
integer reaper.JS_ListView_GetItemState(identifier listviewHWND, integer index)
```

State is a bitmask:
1 = focused, 2 = selected. On Windows only, cut-and-paste marked = 4, drag-and-drop highlighted = 8.
## JS_ListView_GetItemText
```
string text = reaper.JS_ListView_GetItemText(identifier listviewHWND, integer index, integer subItem)
```

No description available.
## JS_ListView_GetSelectedCount
```
integer reaper.JS_ListView_GetSelectedCount(identifier listviewHWND)
```

No description available.
## JS_ListView_GetTopIndex
```
integer reaper.JS_ListView_GetTopIndex(identifier listviewHWND)
```

No description available.
## JS_ListView_HitTest
```
integer index, integer subItem, integer flags = reaper.JS_ListView_HitTest(identifier listviewHWND, integer clientX, integer clientY)
```

No description available.
## JS_ListView_ListAllSelItems
```
integer retval, string items = reaper.JS_ListView_ListAllSelItems(identifier listviewHWND)
```

Returns the indices of all selected items as a comma-separated list.
## JS_ListView_SetItemState
```
reaper.JS_ListView_SetItemState(identifier listviewHWND, integer index, integer state, integer mask)
```

The mask parameter specifies the state bits that must be set, and the state parameter specifies the new values for those bits.
## JS_ListView_SetItemText
```
reaper.JS_ListView_SetItemText(identifier listviewHWND, integer index, integer subItem, string text)
```

Currently, this fuction only accepts ASCII text.
## JS_Localize
```
string translation = reaper.JS_Localize(string USEnglish, string LangPackSection)
```

Returns the translation of the given US English text, according to the currently loaded Language Pack.
## JS_MIDIEditor_ArrayAll
```
integer reaper.JS_MIDIEditor_ArrayAll(identifier reaperarray)
```

Finds all open MIDI windows (whether docked or not).
## JS_MIDIEditor_ListAll
```
integer retval, string list = reaper.JS_MIDIEditor_ListAll()
```

Finds all open MIDI windows (whether docked or not).
## JS_Mem_Alloc
```
identifier reaper.JS_Mem_Alloc(integer sizeBytes)
```

Allocates memory for general use by functions that require memory buffers.
## JS_Mem_Free
```
boolean reaper.JS_Mem_Free(identifier mallocPointer)
```

Frees memory that was previously allocated by JS_Mem_Alloc.
## JS_Mem_FromString
```
boolean reaper.JS_Mem_FromString(identifier mallocPointer, integer offset, string packedString, integer stringLength)
```

Copies a packed string into a memory buffer.
## JS_Mouse_GetCursor
```
identifier reaper.JS_Mouse_GetCursor()
```

On Windows, retrieves a handle to the current mouse cursor.
On Linux and macOS, retrieves a handle to the last cursor set by REAPER or its extensions via SWELL.
## JS_Mouse_GetState
```
integer reaper.JS_Mouse_GetState(integer flags)
```

Retrieves the states of mouse buttons and modifiers keys.
## JS_Mouse_LoadCursor
```
identifier reaper.JS_Mouse_LoadCursor(integer cursorNumber)
```

Loads a cursor by number.
## JS_Mouse_LoadCursorFromFile
```
identifier reaper.JS_Mouse_LoadCursorFromFile(string pathAndFileName, unsupported forceNewLoad)
```

Loads a cursor from a .cur file.
## JS_Mouse_SetCursor
```
reaper.JS_Mouse_SetCursor(identifier cursorHandle)
```

Sets the mouse cursor. (Only lasts while script is running, and for a single "defer" cycle.)
## JS_Mouse_SetPosition
```
boolean reaper.JS_Mouse_SetPosition(integer x, integer y)
```

Moves the mouse cursor to the specified screen coordinates.
## JS_ReaScriptAPI_Version
```
number version = reaper.JS_ReaScriptAPI_Version()
```

Returns the version of the js_ReaScriptAPI extension.
## JS_String
```
boolean retval, string buf = reaper.JS_String(identifier pointer, integer offset, integer lengthChars)
```

Returns the memory contents starting at address[offset] as a packed string. Offset is added as steps of 1 byte (char) each.
## JS_VKeys_GetDown
```
string state = reaper.JS_VKeys_GetDown(number cutoffTime)
```

Returns a 255-byte array that specifies which virtual keys, from 0x01 to 0xFF, have sent KEYDOWN messages since cutoffTime.
## JS_VKeys_GetState
```
string state = reaper.JS_VKeys_GetState(number cutoffTime)
```

Retrieves the current states (0 or 1) of all virtual keys, from 0x01 to 0xFF, in a 255-byte array.
## JS_VKeys_GetUp
```
string state = reaper.JS_VKeys_GetUp(number cutoffTime)
```

Return a 255-byte array that specifies which virtual keys, from 0x01 to 0xFF, have sent KEYUP messages since cutoffTime.
## JS_VKeys_Intercept
```
integer reaper.JS_VKeys_Intercept(integer keyCode, integer intercept)
```

Intercepting (blocking) virtual keys work similar to the native function PreventUIRefresh: Each key has a (non-negative) intercept state, and the key is passed through as usual if the state equals 0, or blocked if the state is greater than 0.
## JS_WindowMessage_Intercept
```
integer reaper.JS_WindowMessage_Intercept(identifier windowHWND, string message, boolean passThrough)
```

Begins intercepting a window message type to specified window.
## JS_WindowMessage_InterceptList
```
integer reaper.JS_WindowMessage_InterceptList(identifier windowHWND, string messages)
```

Begins intercepting window messages to specified window.
## JS_WindowMessage_ListIntercepts
```
boolean retval, string list = reaper.JS_WindowMessage_ListIntercepts(identifier windowHWND)
```

Returns a string with a list of all message types currently being intercepted for the specified window.
## JS_WindowMessage_PassThrough
```
integer reaper.JS_WindowMessage_PassThrough(identifier windowHWND, string message, boolean passThrough)
```

Changes the passthrough setting of a message type that is already being intercepted.
## JS_WindowMessage_Peek
```
boolean retval, boolean passedThrough, number time, integer wParamLow, integer wParamHigh, integer lParamLow, integer lParamHigh = reaper.JS_WindowMessage_Peek(identifier windowHWND, string message)
```

Polls the state of an intercepted message.
## JS_WindowMessage_Post
```
boolean reaper.JS_WindowMessage_Post(identifier windowHWND, string message, number wParam, integer wParamHighWord, number lParam, integer lParamHighWord)
```

If the specified window and message type are not currently being intercepted by a script, this function will post the message in the message queue of the specified window, and return without waiting.
## JS_WindowMessage_Release
```
integer reaper.JS_WindowMessage_Release(identifier windowHWND, string messages)
```

Release intercepts of specified message types.
## JS_WindowMessage_ReleaseAll
```
reaper.JS_WindowMessage_ReleaseAll()
```

Release script intercepts of window messages for all windows.
## JS_WindowMessage_ReleaseWindow
```
reaper.JS_WindowMessage_ReleaseWindow(identifier windowHWND)
```

Release script intercepts of window messages for specified window.
## JS_WindowMessage_Send
```
integer reaper.JS_WindowMessage_Send(identifier windowHWND, string message, number wParam, integer wParamHighWord, number lParam, integer lParamHighWord)
```

Sends a message to the specified window by calling the window process directly, and only returns after the message has been processed. Any intercepts of the message by scripts will be skipped, and the message can therefore not be blocked.
## JS_Window_AddressFromHandle
```
number address = reaper.JS_Window_AddressFromHandle(identifier handle)
```

No description available.
## JS_Window_ArrayAllChild
```
integer reaper.JS_Window_ArrayAllChild(identifier parentHWND, identifier reaperarray)
```

Finds all child windows of the specified parent.
## JS_Window_ArrayAllTop
```
integer reaper.JS_Window_ArrayAllTop(identifier reaperarray)
```

Finds all top-level windows.
## JS_Window_ArrayFind
```
integer reaper.JS_Window_ArrayFind(string title, boolean exact, identifier reaperarray)
```

Finds all windows, whether top-level or child, whose titles match the specified string.
## JS_Window_AttachResizeGrip
```
reaper.JS_Window_AttachResizeGrip(identifier windowHWND)
```

No description available.
## JS_Window_AttachTopmostPin
```
reaper.JS_Window_AttachTopmostPin(identifier windowHWND)
```

Attaches a "pin on top" button to the window frame. The button should remember its state when closing and re-opening the window.
## JS_Window_ClientToScreen
```
integer x, integer y = reaper.JS_Window_ClientToScreen(identifier windowHWND, integer x, integer y)
```

Converts the client-area coordinates of a specified point to screen coordinates.
## JS_Window_Create
```
identifier retval, optional string style = reaper.JS_Window_Create(string title, string className, integer x, integer y, integer w, integer h, optional string style, identifier ownerHWND)
```

Creates a modeless window with WS_OVERLAPPEDWINDOW style and only rudimentary features. Scripts can paint into the window using GDI or LICE/Composite functions (and JS_Window_InvalidateRect to trigger re-painting).
## JS_Window_Destroy
```
reaper.JS_Window_Destroy(identifier windowHWND)
```

Destroys the specified window.
## JS_Window_Enable
```
reaper.JS_Window_Enable(identifier windowHWND, boolean enable)
```

Enables or disables mouse and keyboard input to the specified window or control.
## JS_Window_EnableMetal
```
integer reaper.JS_Window_EnableMetal(identifier windowHWND)
```

On macOS, returns the Metal graphics setting:
2 = Metal enabled and support GetDC()/ReleaseDC() for drawing (more overhead).
1 = Metal enabled.
0 = N/A (Windows and Linux).
-1 = non-metal async layered mode.
-2 = non-metal non-async layered mode.
## JS_Window_Find
```
identifier reaper.JS_Window_Find(string title, boolean exact)
```

Returns a HWND to a window whose title matches the specified string. * Unlike the Win32 function FindWindow, this function searches top-level as well as child windows, so that the target window can be found irrespective of docked state. * In addition, the function can optionally match substrings of the title. * Matching is not case sensitive.
## JS_Window_FindChild
```
identifier reaper.JS_Window_FindChild(identifier parentHWND, string title, boolean exact)
```

Returns a HWND to a child window whose title matches the specified string.
## JS_Window_FindChildByID
```
identifier reaper.JS_Window_FindChildByID(identifier parentHWND, integer ID)
```

Similar to the C++ WIN32 function GetDlgItem, this function finds child windows by ID.
## JS_Window_FindEx
```
identifier reaper.JS_Window_FindEx(identifier parentHWND, identifier childHWND, string className, string title)
```

Returns a handle to a child window whose class and title match the specified strings.
## JS_Window_FindTop
```
identifier reaper.JS_Window_FindTop(string title, boolean exact)
```

Returns a HWND to a top-level window whose title matches the specified string.
## JS_Window_FromPoint
```
identifier reaper.JS_Window_FromPoint(integer x, integer y)
```

Retrieves a HWND to the window that contains the specified point.
## JS_Window_GetClassName
```
string class = reaper.JS_Window_GetClassName(identifier windowHWND)
```

WARNING: May not be fully implemented on macOS and Linux.
## JS_Window_GetClientRect
```
boolean retval, integer left, integer top, integer right, integer bottom = reaper.JS_Window_GetClientRect(identifier windowHWND)
```

Retrieves the screen coordinates of the client area rectangle of the specified window.
## JS_Window_GetClientSize
```
boolean retval, integer width, integer height = reaper.JS_Window_GetClientSize(identifier windowHWND)
```

No description available.
## JS_Window_GetFocus
```
identifier reaper.JS_Window_GetFocus()
```

Retrieves a HWND to the window that has the keyboard focus, if the window is attached to the calling thread's message queue.
## JS_Window_GetForeground
```
identifier reaper.JS_Window_GetForeground()
```

Retrieves a HWND to the top-level foreground window (the window with which the user is currently working).
## JS_Window_GetLong
```
number retval = reaper.JS_Window_GetLong(identifier windowHWND, string info)
```

Similar to JS_Window_GetLongPtr, but returns the information as a number instead of a pointer.
## JS_Window_GetLongPtr
```
identifier reaper.JS_Window_GetLongPtr(identifier windowHWND, string info)
```

Returns information about the specified window.
## JS_Window_GetParent
```
identifier reaper.JS_Window_GetParent(identifier windowHWND)
```

Retrieves a HWND to the specified window's parent or owner.
Returns NULL if the window is unowned or if the function otherwise fails.
## JS_Window_GetRect
```
boolean retval, integer left, integer top, integer right, integer bottom = reaper.JS_Window_GetRect(identifier windowHWND)
```

Retrieves the screen coordinates of the bounding rectangle of the specified window.
## JS_Window_GetRelated
```
identifier reaper.JS_Window_GetRelated(identifier windowHWND, string relation)
```

Retrieves a handle to a window that has the specified relationship (Z-Order or owner) to the specified window.
relation: "LAST", "NEXT", "PREV", "OWNER" or "CHILD".
(Refer to documentation for Win32 C++ function GetWindow.)
## JS_Window_GetScrollInfo
```
boolean retval, integer position, integer pageSize, integer min, integer max, integer trackPos = reaper.JS_Window_GetScrollInfo(identifier windowHWND, string scrollbar)
```

Retrieves the scroll information of a window.
## JS_Window_GetTitle
```
string title = reaper.JS_Window_GetTitle(identifier windowHWND)
```

Returns the title (if any) of the specified window.
## JS_Window_GetViewportFromRect
```
integer left, integer top, integer right, integer bottom = reaper.JS_Window_GetViewportFromRect(integer x1, integer y1, integer x2, integer y2, boolean wantWork)
```

Retrieves the dimensions of the display monitor that has the largest area of intersection with the specified rectangle.
## JS_Window_HandleFromAddress
```
identifier reaper.JS_Window_HandleFromAddress(number address)
```

Converts an address to a handle (such as a HWND) that can be utilized by REAPER and other API functions.
## JS_Window_InvalidateRect
```
boolean reaper.JS_Window_InvalidateRect(identifier windowHWND, integer left, integer top, integer right, integer bottom, boolean eraseBackground)
```

Similar to the Win32 function InvalidateRect.
## JS_Window_IsChild
```
boolean reaper.JS_Window_IsChild(identifier parentHWND, identifier childHWND)
```

Determines whether a window is a child window or descendant window of a specified parent window.
## JS_Window_IsVisible
```
boolean reaper.JS_Window_IsVisible(identifier windowHWND)
```

Determines the visibility state of the window.
## JS_Window_IsWindow
```
boolean reaper.JS_Window_IsWindow(identifier windowHWND)
```

Determines whether the specified window handle identifies an existing window.
## JS_Window_ListAllChild
```
integer retval, string list = reaper.JS_Window_ListAllChild(identifier parentHWND)
```

Finds all child windows of the specified parent.
## JS_Window_ListAllTop
```
integer retval, string list = reaper.JS_Window_ListAllTop()
```

Finds all top-level windows.
## JS_Window_ListFind
```
integer retval, string list = reaper.JS_Window_ListFind(string title, boolean exact)
```

Finds all windows (whether top-level or child) whose titles match the specified string.
## JS_Window_MonitorFromRect
```
integer left, integer top, integer right, integer bottom = reaper.JS_Window_MonitorFromRect(integer x1, integer y1, integer x2, integer y2, boolean wantWork)
```

Deprecated - use GetViewportFromRect instead.
## JS_Window_Move
```
reaper.JS_Window_Move(identifier windowHWND, integer left, integer top)
```

Changes the position of the specified window, keeping its size constant.
## JS_Window_OnCommand
```
boolean reaper.JS_Window_OnCommand(identifier windowHWND, integer commandID)
```

Sends a "WM_COMMAND" message to the specified window, which simulates a user selecting a command in the window menu.
## JS_Window_Resize
```
reaper.JS_Window_Resize(identifier windowHWND, integer width, integer height)
```

Changes the dimensions of the specified window, keeping the top left corner position constant. * If resizing script GUIs, call gfx.update() after resizing.
* Equivalent to calling JS_Window_SetPosition with NOMOVE, NOZORDER, NOACTIVATE and NOOWNERZORDER flags set.
## JS_Window_ScreenToClient
```
integer x, integer y = reaper.JS_Window_ScreenToClient(identifier windowHWND, integer x, integer y)
```

Converts the screen coordinates of a specified point on the screen to client-area coordinates.
## JS_Window_SetFocus
```
reaper.JS_Window_SetFocus(identifier windowHWND)
```

Sets the keyboard focus to the specified window.
## JS_Window_SetForeground
```
reaper.JS_Window_SetForeground(identifier windowHWND)
```

Brings the specified window into the foreground, activates the window, and directs keyboard input to it.
## JS_Window_SetLong
```
number retval = reaper.JS_Window_SetLong(identifier windowHWND, string info, number value)
```

Similar to the Win32 function SetWindowLongPtr.
## JS_Window_SetOpacity
```
boolean reaper.JS_Window_SetOpacity(identifier windowHWND, string mode, number value)
```

Sets the window opacity.
## JS_Window_SetParent
```
identifier reaper.JS_Window_SetParent(identifier childHWND, identifier parentHWND)
```

If successful, returns a handle to the previous parent window.
## JS_Window_SetPosition
```
boolean retval, optional string ZOrder, optional string flags = reaper.JS_Window_SetPosition(identifier windowHWND, integer left, integer top, integer width, integer height, optional string ZOrder, optional string flags)
```

Interface to the Win32/swell function SetWindowPos, with which window position, size, Z-order and visibility can be set, and new frame styles can be applied.
## JS_Window_SetScrollPos
```
boolean reaper.JS_Window_SetScrollPos(identifier windowHWND, string scrollbar, integer position)
```

Parameters: * scrollbar: "v" (or "SB_VERT", or "VERT") for vertical scroll, "h" (or "SB_HORZ" or "HORZ") for horizontal.
## JS_Window_SetStyle
```
boolean retval, string style = reaper.JS_Window_SetStyle(identifier windowHWND, string style)
```

Sets and applies a window style.
## JS_Window_SetTitle
```
boolean reaper.JS_Window_SetTitle(identifier windowHWND, string title)
```

Changes the title of the specified window. Returns true if successful.
## JS_Window_SetZOrder
```
boolean reaper.JS_Window_SetZOrder(identifier windowHWND, string ZOrder, identifier insertAfterHWND)
```

Sets the window Z order. * Equivalent to calling JS_Window_SetPos with flags NOMOVE | NOSIZE. * Not all the Z orders have been implemented in Linux yet.
## JS_Window_Show
```
reaper.JS_Window_Show(identifier windowHWND, string state)
```

Sets the specified window's show state.
## JS_Window_Update
```
reaper.JS_Window_Update(identifier windowHWND)
```

Similar to the Win32 function UpdateWindow.
## JS_Zip_Close
```
integer reaper.JS_Zip_Close(string zipFile, identifier zipHandle)
```

Closes the zip archive, using either the file name or the zip handle. Finalizes entries and releases resources.
## JS_Zip_CountEntries
```
integer reaper.JS_Zip_CountEntries(identifier zipHandle)
```

No description available.
## JS_Zip_DeleteEntries
```
integer reaper.JS_Zip_DeleteEntries(identifier zipHandle, string entryNames, integer entryNamesStrLen)
```

Deletes the specified entries from an existing Zip file.
## JS_Zip_Entry_Close
```
integer reaper.JS_Zip_Entry_Close(identifier zipHandle)
```

Closes a zip entry, flushes buffer and releases resources. In WRITE mode, entries must be closed in order to apply and save changes.
## JS_Zip_Entry_CompressFile
```
integer reaper.JS_Zip_Entry_CompressFile(identifier zipHandle, string inputFile)
```

Compresses the specified file into the zip archive's open entry.
## JS_Zip_Entry_CompressMemory
```
integer reaper.JS_Zip_Entry_CompressMemory(identifier zipHandle, string buf, integer buf_size)
```

Compresses the specified memory buffer into the zip archive's open entry.
## JS_Zip_Entry_ExtractToFile
```
integer reaper.JS_Zip_Entry_ExtractToFile(identifier zipHandle, string outputFile)
```

Extracts the zip archive's open entry.
## JS_Zip_Entry_ExtractToMemory
```
integer retval, string contents = reaper.JS_Zip_Entry_ExtractToMemory(identifier zipHandle)
```

Extracts and returns the zip archive's open entry.
## JS_Zip_Entry_Info
```
integer retval, string name, integer index, integer isFolder, number size, number crc32 = reaper.JS_Zip_Entry_Info(identifier zipHandle)
```

Returns information about the zip archive's open entry.
## JS_Zip_Entry_OpenByIndex
```
integer reaper.JS_Zip_Entry_OpenByIndex(identifier zipHandle, integer index)
```

Opens a new entry by index in the zip archive.
## JS_Zip_Entry_OpenByName
```
integer reaper.JS_Zip_Entry_OpenByName(identifier zipHandle, string entryName)
```

Opens an entry by name in the zip archive.
## JS_Zip_ErrorString
```
string errorStr = reaper.JS_Zip_ErrorString(integer errorNum)
```

Returns a descriptive string for the given error code.
## JS_Zip_Extract
```
integer reaper.JS_Zip_Extract(string zipFile, string outputFolder)
```

Extracts an existing Zip file to the specified folder.
## JS_Zip_ListAllEntries
```
integer retval, string list = reaper.JS_Zip_ListAllEntries(identifier zipHandle)
```

Returns the number of entries and a zero-separated and double-zero-terminated string of entry names.
## JS_Zip_Open
```
identifier retval, integer retval = reaper.JS_Zip_Open(string zipFile, string mode, integer compressionLevel)
```

Opens a zip archive using the given mode, which can be either "READ" or "WRITE" (or simply 'r' or 'w').
## Llm_Do
```
reaper.Llm_Do()
```

Do. Call this function to run one ReaLlm cycle. Use this function to run ReaLlm on arbitrary time intervals e.g. from a deferred script.
## Llm_GetPaths
```
string pathString = reaper.Llm_GetPaths(boolean includeFx, MediaTrack startIn, MediaTrack endIn)
```

Get paths. Returns a string of the form "start:fx#1.fx#2...;track:fxs;...;end:fxs" where track is the track number and fx is the fx index. The string is truncated to pathStringOut_sz. 1-based indexing is used. If no MediaTrack* start is provided, all monitored input tracks are used. If no MediaTrack* end is provided, all hardware output tracks are used. If includeFx is true, the fx indices are included.
## Llm_GetSafed
```
string safeString = reaper.Llm_GetSafed()
```

Get safed. Returns a string of the form "track:fx;track:fx;..." where track is the track number and fx is the fx index. The string is truncated to safeStringOut_sz. 1-based indexing is used. The string is followed by a | delimited list of fx names that have been set safed.
## Llm_GetVersion
```
integer major, integer minor, integer patch, integer build, string commit = reaper.Llm_GetVersion()
```

Get version. Returns the version of the plugin as integers and the commit hash as a string. The string is truncated to commitOut_sz.
## Llm_SetClearSafe
```
reaper.Llm_SetClearSafe(boolean clear_manually_safed_fx)
```

Set clear safe. Set clear_manually_safed_fx = true to clear manually safed fx
## Llm_SetKeepPdc
```
reaper.Llm_SetKeepPdc(boolean enable)
```

Set keep pdc
## Llm_SetMonitoringFX
```
reaper.Llm_SetMonitoringFX(boolean enable)
```

Set to include MonitoringFX. In REAPER land this means the fx on the master track record fx chain. Indexed as fx# + 0x1000000, 0-based.
## Llm_SetParameterChange
```
reaper.Llm_SetParameterChange(string fx_name, integer parameter_index, number val1, number val2)
```

Set parameter change. Set val1 = val2 to clear change. Set parameter_index = -666 to clear all changes. Use this function to set parameter changes between values val1 and val2 for fx_name and parameter_index instead of disabling the effect. Use custom fx names to identify individual fx.
## Llm_SetPdcLimit
```
reaper.Llm_SetPdcLimit(number pdc_factor)
```

Set pdc limit as factor of audio buffer size.
## Llm_SetSafed
```
string fx_name = reaper.Llm_SetSafed(string fx_name, boolean isSet)
```

Set safed. Set isSet = true to safe fx name. Set isSet = false to unsafe fx name.
## MCULive_GetButtonValue
```
integer reaper.MCULive_GetButtonValue(integer device, integer button)
```

Get current button state.
## MCULive_GetDevice
```
integer reaper.MCULive_GetDevice(integer device, integer type)
```

Get MIDI input or output dev ID. type 0 is input dev, type 1 is output dev. device < 0 returns number of MCULive devices.
## MCULive_GetEncoderValue
```
number reaper.MCULive_GetEncoderValue(integer device, integer encIdx, integer param)
```

Returns zero-indexed encoder parameter value. 0 = lastpos, 1 = lasttouch
## MCULive_GetFaderValue
```
number reaper.MCULive_GetFaderValue(integer device, integer faderIdx, integer param)
```

Returns zero-indexed fader parameter value. 0 = lastpos, 1 = lasttouch, 2 = lastmove (any fader)
## MCULive_GetMIDIMessage
```
integer retval, integer status, integer data1, integer data2, integer frame_offset, optional string msg = reaper.MCULive_GetMIDIMessage(integer device, integer msgIdx)
```

Gets MIDI message from input buffer/queue. Gets (pops/pulls) indexed message (status, data1, data2 and frame_offset) from queue and retval is total size/length left in queue. E.g. continuously read all indiviual messages with deferred script. Frame offset resolution is 1/1024000 seconds, not audio samples. Long messages are returned as optional strings of byte characters. msgIdx -1 returns size (length) of buffer. Read also non-MCU devices by creating MCULive device with their input.
## MCULive_Map
```
integer reaper.MCULive_Map(integer device, integer button, integer command_id, boolean isRemap)
```

Maps MCU Live device# button# to REAPER command ID. E.g. reaper.MCULive_Map(0,0x5b, 40340) maps MCU Rewind to "Track: Unsolo all tracks". Or remap button to another button if your MCU button layout doesnt play nicely with default MCULive mappings. By default range 0x00 .. 0x2d is in use. Button numbers are second column (prefixed with 0x) e.g. '90 5e' 0x5e for 'transport : play', roughly.
## MCULive_Reset
```
integer reaper.MCULive_Reset(integer device)
```

Reset device. device < 0 resets all and returns number of devices.
## MCULive_SendMIDIMessage
```
integer reaper.MCULive_SendMIDIMessage(integer device, integer status, integer data1, integer data2, optional string msgIn)
```

Sends MIDI message to device. If string is provided, individual bytes are not sent. Returns number of sent bytes.
## MCULive_SetButtonPassthrough
```
integer reaper.MCULive_SetButtonPassthrough(integer device, integer button, boolean isSet)
```

Set button as MIDI passthrough.
## MCULive_SetButtonPressOnly
```
integer reaper.MCULive_SetButtonPressOnly(integer device, integer button, boolean isSet)
```

Buttons function as press only by default. Set false for press and release function.
## MCULive_SetButtonValue
```
integer reaper.MCULive_SetButtonValue(integer device, integer button, integer value)
```

Set button led/mode/state. Value 0 = off,1 = blink, 0x7f = on, usually.
## MCULive_SetDefault
```
reaper.MCULive_SetDefault(integer device, boolean isSet)
```

Enables/disables default out-of-the-box operation.
## MCULive_SetDisplay
```
reaper.MCULive_SetDisplay(integer device, integer pos, string message, integer pad)
```

Write to display. 112 characters, 56 per row.
## MCULive_SetEncoderValue
```
integer reaper.MCULive_SetEncoderValue(integer device, integer encIdx, number val, integer type)
```

Set encoder to value 0 ... 1.0. Type 0 = linear, 1 = track volume, 2 = pan. Returns scaled value.
## MCULive_SetFaderValue
```
integer reaper.MCULive_SetFaderValue(integer device, integer faderIdx, number val, integer type)
```

Set fader to value 0 ... 1.0. Type 0 = linear, 1 = track volume, 2 = pan. Returns scaled value.
## MCULive_SetMeterValue
```
integer reaper.MCULive_SetMeterValue(integer device, integer meterIdx, number val, integer type)
```

Set meter value 0 ... 1.0. Type 0 = linear, 1 = track volume (with decay).
## MCULive_SetOption
```
reaper.MCULive_SetOption(integer option, integer value)
```

1 : surface split point device index 2 : 'mode-is-global' bitmask/flags, first 6 bits
## MRP_CalculateEnvelopeHash
```
integer reaper.MRP_CalculateEnvelopeHash(TrackEnvelope env)
```

This function isn't really correct... it calculates a 64 bit hash but returns it as a 32 bit int. Should reimplement this. Or rather, even more confusingly : The hash will be 32 bit when building for 32 bit architecture and 64 bit when building for 64 bit architecture! It comes down to how size_t is of different size between the 32 and 64 bit architectures.
## MRP_CastDoubleToInt
```
integer reaper.MRP_CastDoubleToInt(number n1, number n2)
```

add two numbers
## MRP_CreateArray
```
MRP_Array reaper.MRP_CreateArray(integer size)
```

Create an array of 64 bit floating point numbers. Note that these will leak memory if they are not later destroyed with MRP_DestroyArray!
## MRP_CreateWindow
```
MRP_Window reaper.MRP_CreateWindow(string title)
```

Create window
## MRP_DestroyArray
```
reaper.MRP_DestroyArray(MRP_Array array)
```

Destroy a previously created MRP_Array
## MRP_DestroyWindow
```
reaper.MRP_DestroyWindow(MRP_Window window)
```

Destroy window
## MRP_DoNothing
```
reaper.MRP_DoNothing()
```

do nothing, return null
## MRP_DoublePointer
```
number reaper.MRP_DoublePointer(number n1, number n2)
```

add two numbers
## MRP_DoublePointerAsInt
```
integer reaper.MRP_DoublePointerAsInt(number n1, number n2)
```

add two numbers
## MRP_GenerateSine
```
reaper.MRP_GenerateSine(MRP_Array array, number samplerate, number frequency)
```

Generate a sine wave into a MRP_Array
## MRP_GetArrayValue
```
number reaper.MRP_GetArrayValue(MRP_Array array, integer index)
```

Get MRP_Array element value. No safety checks done for array or index validity, so use at your own peril!
## MRP_GetControlFloatNumber
```
number reaper.MRP_GetControlFloatNumber(MRP_Window window, string controlname, integer which)
```

Get a floating point number associated with control. Meaning of 'which' depends on the control targeted.
## MRP_GetControlIntNumber
```
integer reaper.MRP_GetControlIntNumber(MRP_Window window, string controlname, integer which)
```

Get an integer point number associated with control. Meaning of 'which' depends on the control targeted.
## MRP_GetWindowDirty
```
boolean reaper.MRP_GetWindowDirty(MRP_Window window, integer whichdirty)
```

Get window dirty state (ie, if something was changed in the window). which : 0 window size
## MRP_GetWindowPosSizeValue
```
integer reaper.MRP_GetWindowPosSizeValue(MRP_Window window, integer which)
```

Get window geometry values. which : 0 x, 1 y, 2 w, 3 h
## MRP_IntPointer
```
integer reaper.MRP_IntPointer(integer n1, integer n2)
```

add two numbers
## MRP_MultiplyArrays
```
reaper.MRP_MultiplyArrays(MRP_Array array1, MRP_Array array2, MRP_Array array3)
```

Multiply 2 MRP_Arrays of same length. Result is written to 3rd array.
## MRP_MultiplyArraysMT
```
reaper.MRP_MultiplyArraysMT(MRP_Array array1, MRP_Array array2, MRP_Array array3)
```

Multiply 2 MRP_Arrays of same length. Result is written to 3rd array. Uses multiple threads.
## MRP_ReturnMediaItem
```
MediaItem reaper.MRP_ReturnMediaItem()
```

return media item
## MRP_SendCommandString
```
reaper.MRP_SendCommandString(MRP_Window window, string controlname, string commandtext)
```

Send a command message to control. Currently only the envelope control understands some messages.
## MRP_SetArrayValue
```
reaper.MRP_SetArrayValue(MRP_Array array, integer index, number value)
```

Set MRP_Array element value. No safety checks done for array or index validity, so use at your own peril!
## MRP_SetControlBounds
```
reaper.MRP_SetControlBounds(MRP_Window window, string name, number x, number y, number w, number h)
```

Set MRP control position and size
## MRP_SetControlFloatNumber
```
reaper.MRP_SetControlFloatNumber(MRP_Window window, string controlname, integer which, number value)
```

Set a floating point number associated with control. Meaning of 'which' depends on the control targeted.
## MRP_SetControlIntNumber
```
reaper.MRP_SetControlIntNumber(MRP_Window window, string controlname, integer which, integer value)
```

Set an integer point number associated with control. Meaning of 'which' depends on the control targeted.
## MRP_SetControlString
```
reaper.MRP_SetControlString(MRP_Window window, string controlname, integer which, string text)
```

Set a text property associated with control. Meaning of 'which' depends on the control targeted.
## MRP_SetWindowDirty
```
reaper.MRP_SetWindowDirty(MRP_Window window, integer which, boolean state)
```

Set window dirty state (ie, if something was changed in the controls)
## MRP_WindowAddControl
```
reaper.MRP_WindowAddControl(MRP_Window window, string controltypename, string objectname)
```

Add a control to window. Controltypename is the type of control to create. Objectname must be a unique id
## MRP_WindowClearDirtyControls
```
reaper.MRP_WindowClearDirtyControls(MRP_Window window)
```

Clears the dirty states of the controls in a window.
## MRP_WindowIsClosed
```
boolean reaper.MRP_WindowIsClosed(MRP_Window window)
```

Returns if the window has been closed and the ReaScript defer loop should likely be exited
## MRP_WindowIsDirtyControl
```
boolean reaper.MRP_WindowIsDirtyControl(MRP_Window window, string controlname)
```

Returns true if control was manipulated
## MRP_WindowSetTitle
```
reaper.MRP_WindowSetTitle(MRP_Window window, string title)
```

Set window title
## MRP_WriteArrayToFile
```
reaper.MRP_WriteArrayToFile(MRP_Array array, string filename, number samplerate)
```

Write MRP_Array to disk as a 32 bit floating point mono wav file
## NF_AnalyzeMediaItemPeakAndRMS
```
boolean reaper.NF_AnalyzeMediaItemPeakAndRMS(MediaItem item, number windowSize, identifier reaper.array_peaks, identifier reaper.array_peakpositions, identifier reaper.array_RMSs, identifier reaper.array_RMSpositions)
```

This function combines all other NF_Peak/RMS functions in a single one and additionally returns peak RMS positions. Lua example code here. Note: It's recommended to use this function with ReaScript/Lua as it provides reaper.array objects. If using this function with other scripting languages, you must provide arrays in the reaper.array format.
## NF_AnalyzeTakeLoudness
```
boolean retval, number lufsIntegrated, number range, number truePeak, number truePeakPos, number shortTermMax, number momentaryMax = reaper.NF_AnalyzeTakeLoudness(MediaItem_Take take, boolean analyzeTruePeak)
```

Full loudness analysis. retval: returns true on successful analysis, false on MIDI take or when analysis failed for some reason. analyzeTruePeak=true: Also do true peak analysis. Returns true peak value in dBTP and true peak position (relative to item position). Considerably slower than without true peak analysis (since it uses oversampling). Note: Short term uses a time window of 3 sec. for calculation. So for items shorter than this shortTermMaxOut can't be calculated correctly. Momentary uses a time window of 0.4 sec.
## NF_AnalyzeTakeLoudness2
```
boolean retval, number lufsIntegrated, number range, number truePeak, number truePeakPos, number shortTermMax, number momentaryMax, number shortTermMaxPos, number momentaryMaxPos = reaper.NF_AnalyzeTakeLoudness2(MediaItem_Take take, boolean analyzeTruePeak)
```

Same as NF_AnalyzeTakeLoudness but additionally returns shortTermMaxPos and momentaryMaxPos (in absolute project time). Note: shortTermMaxPos and momentaryMaxPos indicate the beginning of time intervalls, (3 sec. and 0.4 sec. resp.).
## NF_AnalyzeTakeLoudness_IntegratedOnly
```
boolean retval, number lufsIntegrated = reaper.NF_AnalyzeTakeLoudness_IntegratedOnly(MediaItem_Take take)
```

Does LUFS integrated analysis only. Faster than full loudness analysis (NF_AnalyzeTakeLoudness) . Use this if only LUFS integrated is required. Take vol. env. is taken into account. See: Signal flow
## NF_Base64_Decode
```
boolean retval, string decodedStr = reaper.NF_Base64_Decode(string base64Str)
```

Returns true on success.
## NF_Base64_Encode
```
string encodedStr = reaper.NF_Base64_Encode(string str, boolean usePadding)
```

Input string may contain null bytes in REAPER 6.44 or newer. Note: Doesn't allow padding in the middle (e.g. concatenated encoded strings), doesn't allow newlines.
## NF_ClearGlobalStartupAction
```
boolean reaper.NF_ClearGlobalStartupAction()
```

Returns true if global startup action was cleared successfully.
## NF_ClearProjectStartupAction
```
boolean reaper.NF_ClearProjectStartupAction()
```

Returns true if project startup action was cleared successfully.
## NF_ClearProjectTrackSelectionAction
```
boolean reaper.NF_ClearProjectTrackSelectionAction()
```

Returns true if project track selection action was cleared successfully.
## NF_DeleteTakeFromItem
```
boolean reaper.NF_DeleteTakeFromItem(MediaItem item, integer takeIdx)
```

Deletes a take from an item. takeIdx is zero-based. Returns true on success.
## NF_GetGlobalStartupAction
```
boolean retval, string desc, string cmdId = reaper.NF_GetGlobalStartupAction()
```

Gets action description and command ID number (for native actions) or named command IDs / identifier strings (for extension actions /ReaScripts) if global startup action is set, otherwise empty string. Returns false on failure.
## NF_GetMediaItemAverageRMS
```
number reaper.NF_GetMediaItemAverageRMS(MediaItem item)
```

Returns the average overall (non-windowed) dB RMS level of active channels of an audio item active take, post item gain, post take volume envelope, post-fade, pre fader, pre item FX. Returns -150.0 if MIDI take or empty item.
## NF_GetMediaItemMaxPeak
```
number reaper.NF_GetMediaItemMaxPeak(MediaItem item)
```

Returns the greatest max. peak value in dBFS of all active channels of an audio item active take, post item gain, post take volume envelope, post-fade, pre fader, pre item FX. Returns -150.0 if MIDI take or empty item.
## NF_GetMediaItemMaxPeakAndMaxPeakPos
```
number retval, number maxPeakPos = reaper.NF_GetMediaItemMaxPeakAndMaxPeakPos(MediaItem item)
```

See NF_GetMediaItemMaxPeak, additionally returns maxPeakPos (relative to item position).
## NF_GetMediaItemPeakRMS_NonWindowed
```
number reaper.NF_GetMediaItemPeakRMS_NonWindowed(MediaItem item)
```

Returns the greatest overall (non-windowed) dB RMS peak level of all active channels of an audio item active take, post item gain, post take volume envelope, post-fade, pre fader, pre item FX. Returns -150.0 if MIDI take or empty item.
## NF_GetMediaItemPeakRMS_Windowed
```
number reaper.NF_GetMediaItemPeakRMS_Windowed(MediaItem item)
```

Returns the average dB RMS peak level of all active channels of an audio item active take, post item gain, post take volume envelope, post-fade, pre fader, pre item FX. Obeys 'Window size for peak RMS' setting in 'SWS: Set RMS analysis/normalize options' for calculation. Returns -150.0 if MIDI take or empty item.
## NF_GetProjectStartupAction
```
boolean retval, string desc, string cmdId = reaper.NF_GetProjectStartupAction()
```

Gets action description and command ID number (for native actions) or named command IDs / identifier strings (for extension actions /ReaScripts) if project startup action is set, otherwise empty string. Returns false on failure.
## NF_GetProjectTrackSelectionAction
```
boolean retval, string desc, string cmdId = reaper.NF_GetProjectTrackSelectionAction()
```

Gets action description and command ID number (for native actions) or named command IDs / identifier strings (for extension actions /ReaScripts) if project track selection action is set, otherwise empty string. Returns false on failure.
## NF_GetSWSMarkerRegionSub
```
string reaper.NF_GetSWSMarkerRegionSub(integer markerRegionIdx)
```

Returns SWS/S&M marker/region subtitle. markerRegionIdx: Refers to index that can be passed to EnumProjectMarkers (not displayed marker/region index). Returns empty string if marker/region with specified index not found or marker/region subtitle not set. Lua code example here.
## NF_GetSWSTrackNotes
```
string reaper.NF_GetSWSTrackNotes(MediaTrack track)
```

No description available.
## NF_GetSWS_RMSoptions
```
number target, number windowSize = reaper.NF_GetSWS_RMSoptions()
```

Get SWS analysis/normalize options. See NF_SetSWS_RMSoptions.
## NF_GetThemeDefaultTCPHeights
```
integer supercollapsed, integer collapsed, integer small, integer recarm = reaper.NF_GetThemeDefaultTCPHeights()
```

No description available.
## NF_ReadAudioFileBitrate
```
integer reaper.NF_ReadAudioFileBitrate(string fn)
```

Returns the bitrate of an audio file in kb/s if available (0 otherwise). For supported filetypes see TagLib::AudioProperties::bitrate.
## NF_ScrollHorizontallyByPercentage
```
reaper.NF_ScrollHorizontallyByPercentage(integer amount)
```

100 means scroll one page. Negative values scroll left.
## NF_SetGlobalStartupAction
```
boolean reaper.NF_SetGlobalStartupAction(string str)
```

Returns true if global startup action was set successfully (i.e. valid action ID). Note: For SWS / S&M actions and macros / scripts, you must use identifier strings (e.g. "_SWS_ABOUT", "_f506bc780a0ab34b8fdedb67ed5d3649"), not command IDs (e.g. "47145").
Tip: to copy such identifiers, right-click the action in the Actions window > Copy selected action cmdID / identifier string.
NOnly works for actions / scripts from Main action section.
## NF_SetProjectStartupAction
```
boolean reaper.NF_SetProjectStartupAction(string str)
```

Returns true if project startup action was set successfully (i.e. valid action ID). Note: For SWS / S&M actions and macros / scripts, you must use identifier strings (e.g. "_SWS_ABOUT", "_f506bc780a0ab34b8fdedb67ed5d3649"), not command IDs (e.g. "47145").
Tip: to copy such identifiers, right-click the action in the Actions window > Copy selected action cmdID / identifier string.
Only works for actions / scripts from Main action section. Project must be saved after setting project startup action to be persistent.
## NF_SetProjectTrackSelectionAction
```
boolean reaper.NF_SetProjectTrackSelectionAction(string str)
```

Returns true if project track selection action was set successfully (i.e. valid action ID). Note: For SWS / S&M actions and macros / scripts, you must use identifier strings (e.g. "_SWS_ABOUT", "_f506bc780a0ab34b8fdedb67ed5d3649"), not command IDs (e.g. "47145").
Tip: to copy such identifiers, right-click the action in the Actions window > Copy selected action cmdID / identifier string.
Only works for actions / scripts from Main action section. Project must be saved after setting project track selection action to be persistent.
## NF_SetSWSMarkerRegionSub
```
boolean reaper.NF_SetSWSMarkerRegionSub(string markerRegionSub, integer markerRegionIdx)
```

Set SWS/S&M marker/region subtitle. markerRegionIdx: Refers to index that can be passed to EnumProjectMarkers (not displayed marker/region index). Returns true if subtitle is set successfully (i.e. marker/region with specified index is present in project). Lua code example here.
## NF_SetSWSTrackNotes
```
reaper.NF_SetSWSTrackNotes(MediaTrack track, string str)
```

No description available.
## NF_SetSWS_RMSoptions
```
boolean reaper.NF_SetSWS_RMSoptions(number targetLevel, number windowSize)
```

Set SWS analysis/normalize options (same as running action 'SWS: Set RMS analysis/normalize options'). targetLevel: target RMS normalize level (dB), windowSize: window size for peak RMS (sec.)
## NF_TakeFX_GetFXModuleName
```
boolean retval, string name = reaper.NF_TakeFX_GetFXModuleName(MediaItem item, integer fx)
```

Deprecated, see TakeFX_GetNamedConfigParm/'fx_ident' (v6.37+). See BR_TrackFX_GetFXModuleName. fx: counted consecutively across all takes (zero-based).
## NF_UpdateSWSMarkerRegionSubWindow
```
reaper.NF_UpdateSWSMarkerRegionSubWindow()
```

Redraw the Notes window (call if you've changed a subtitle via NF_SetSWSMarkerRegionSub which is currently displayed in the Notes window and you want to appear the new subtitle immediately.)
## NF_Win32_GetSystemMetrics
```
integer reaper.NF_Win32_GetSystemMetrics(integer nIndex)
```

Equivalent to win32 API GetSystemMetrics(). Note: Only SM_C[XY]SCREEN, SM_C[XY][HV]SCROLL and SM_CYMENU are currently supported on macOS and Linux as of REAPER 6.68. Check the SWELL source code for up-to-date support information (swell-wnd.mm, swell-wnd-generic.cpp).
## ReaPack_AboutInstalledPackage
```
boolean reaper.ReaPack_AboutInstalledPackage(PackageEntry entry)
```

Show the about dialog of the given package entry.
The repository index is downloaded asynchronously if the cached copy doesn't exist or is older than one week.
## ReaPack_AboutRepository
```
boolean reaper.ReaPack_AboutRepository(string repoName)
```

Show the about dialog of the given repository. Returns true if the repository exists in the user configuration.
The repository index is downloaded asynchronously if the cached copy doesn't exist or is older than one week.
## ReaPack_AddSetRepository
```
boolean retval, string error = reaper.ReaPack_AddSetRepository(string name, string url, boolean enable, integer autoInstall)
```

Add or modify a repository. Set url to nullptr (or empty string in Lua) to keep the existing URL. Call ReaPack_ProcessQueue(true) when done to process the new list and update the GUI.
## ReaPack_BrowsePackages
```
reaper.ReaPack_BrowsePackages(string filter)
```

Opens the package browser with the given filter string.
## ReaPack_CompareVersions
```
integer retval, string error = reaper.ReaPack_CompareVersions(string ver1, string ver2)
```

Returns 0 if both versions are equal, a positive value if ver1 is higher than ver2 and a negative value otherwise.
## ReaPack_EnumOwnedFiles
```
boolean retval, string path, integer sections, integer type = reaper.ReaPack_EnumOwnedFiles(PackageEntry entry, integer index)
```

Enumerate the files owned by the given package. Returns false when there is no more data.
## ReaPack_FreeEntry
```
boolean reaper.ReaPack_FreeEntry(PackageEntry entry)
```

Free resources allocated for the given package entry.
## ReaPack_GetEntryInfo
```
boolean retval, string repo, string cat, string pkg, string desc, integer type, string ver, string author, integer flags, integer fileCount = reaper.ReaPack_GetEntryInfo(PackageEntry entry)
```

Get the repository name, category, package name, package description, package type, the currently installed version, author name, flags (&1=Pinned, &2=BleedingEdge) and how many files are owned by the given package entry.
## ReaPack_GetOwner
```
PackageEntry retval, string error = reaper.ReaPack_GetOwner(string fn)
```

Returns the package entry owning the given file.
Delete the returned object from memory after use with ReaPack_FreeEntry.
## ReaPack_GetRepositoryInfo
```
boolean retval, string url, boolean enabled, integer autoInstall = reaper.ReaPack_GetRepositoryInfo(string name)
```

Get the infos of the given repository.
## ReaPack_ProcessQueue
```
reaper.ReaPack_ProcessQueue(boolean refreshUI)
```

Run pending operations and save the configuration file. If refreshUI is true the browser and manager windows are guaranteed to be refreshed (otherwise it depends on which operations are in the queue).
## SNM_AddReceive
```
boolean reaper.SNM_AddReceive(MediaTrack src, MediaTrack dest, integer type)
```

[S&M] Deprecated, see CreateTrackSend (v5.15pre1+). Adds a receive. Returns false if nothing updated.
type -1=Default type (user preferences), 0=Post-Fader (Post-Pan), 1=Pre-FX, 2=deprecated, 3=Pre-Fader (Post-FX).
Note: obeys default sends preferences, supports frozen tracks, etc..
## SNM_AddTCPFXParm
```
boolean reaper.SNM_AddTCPFXParm(MediaTrack tr, integer fxId, integer prmId)
```

[S&M] Add an FX parameter knob in the TCP. Returns false if nothing updated (invalid parameters, knob already present, etc..)
## SNM_CreateFastString
```
WDL_FastString reaper.SNM_CreateFastString(string str)
```

[S&M] Instantiates a new "fast string". You must delete this string, see SNM_DeleteFastString.
## SNM_DeleteFastString
```
reaper.SNM_DeleteFastString(WDL_FastString str)
```

[S&M] Deletes a "fast string" instance.
## SNM_GetDoubleConfigVar
```
number reaper.SNM_GetDoubleConfigVar(string varname, number errvalue)
```

[S&M] Returns a floating-point preference (look in project prefs first, then in general prefs). Returns errvalue if failed (e.g. varname not found).
## SNM_GetDoubleConfigVarEx
```
number reaper.SNM_GetDoubleConfigVarEx(ReaProject proj, string varname, number errvalue)
```

[S&M] See SNM_GetDoubleConfigVar.
## SNM_GetFastString
```
string reaper.SNM_GetFastString(WDL_FastString str)
```

[S&M] Gets the "fast string" content.
## SNM_GetFastStringLength
```
integer reaper.SNM_GetFastStringLength(WDL_FastString str)
```

[S&M] Gets the "fast string" length.
## SNM_GetIntConfigVar
```
integer reaper.SNM_GetIntConfigVar(string varname, integer errvalue)
```

[S&M] Returns an integer preference (look in project prefs first, then in general prefs). Returns errvalue if failed (e.g. varname not found).
## SNM_GetIntConfigVarEx
```
integer reaper.SNM_GetIntConfigVarEx(ReaProject proj, string varname, integer errvalue)
```

[S&M] See SNM_GetIntConfigVar.
## SNM_GetLongConfigVar
```
boolean retval, integer high, integer low = reaper.SNM_GetLongConfigVar(string varname)
```

[S&M] Reads a 64-bit integer preference split in two 32-bit integers (look in project prefs first, then in general prefs). Returns false if failed (e.g. varname not found).
## SNM_GetLongConfigVarEx
```
boolean retval, integer high, integer low = reaper.SNM_GetLongConfigVarEx(ReaProject proj, string varname)
```

[S&M] See SNM_GetLongConfigVar.
## SNM_GetMediaItemTakeByGUID
```
MediaItem_Take reaper.SNM_GetMediaItemTakeByGUID(ReaProject project, string guid)
```

[S&M] Gets a take by GUID as string. The GUID must be enclosed in braces {}. To get take GUID as string, see BR_GetMediaItemTakeGUID
## SNM_GetProjectMarkerName
```
boolean reaper.SNM_GetProjectMarkerName(ReaProject proj, integer num, boolean isrgn, WDL_FastString name)
```

[S&M] Gets a marker/region name. Returns true if marker/region found.
## SNM_GetSetObjectState
```
boolean reaper.SNM_GetSetObjectState(identifier obj, WDL_FastString state, boolean setnewvalue, boolean wantminimalstate)
```

[S&M] Gets or sets the state of a track, an item or an envelope. The state chunk size is unlimited. Returns false if failed.
When getting a track state (and when you are not interested in FX data), you can use wantminimalstate=true to radically reduce the length of the state. Do not set such minimal states back though, this is for read-only applications!
Note: unlike the native GetSetObjectState, calling to FreeHeapPtr() is not required.
## SNM_GetSetSourceState
```
boolean reaper.SNM_GetSetSourceState(MediaItem item, integer takeidx, WDL_FastString state, boolean setnewvalue)
```

[S&M] Gets or sets a take source state. Returns false if failed. Use takeidx=-1 to get/alter the active take.
Note: this function does not use a MediaItem_Take* param in order to manage empty takes (i.e. takes with MediaItem_Take*==NULL), see SNM_GetSetSourceState2.
## SNM_GetSetSourceState2
```
boolean reaper.SNM_GetSetSourceState2(MediaItem_Take take, WDL_FastString state, boolean setnewvalue)
```

[S&M] Gets or sets a take source state. Returns false if failed.
Note: this function cannot deal with empty takes, see SNM_GetSetSourceState.
## SNM_GetSourceType
```
boolean reaper.SNM_GetSourceType(MediaItem_Take take, WDL_FastString type)
```

[S&M] Deprecated, see GetMediaSourceType. Gets the source type of a take. Returns false if failed (e.g. take with empty source, etc..)
## SNM_MoveOrRemoveTrackFX
```
boolean reaper.SNM_MoveOrRemoveTrackFX(MediaTrack tr, integer fxId, integer what)
```

[S&M] Deprecated, see TrackFX_{CopyToTrack,Delete} (v5.95+). Move or removes a track FX. Returns true if tr has been updated.
fxId: fx index in chain or -1 for the selected fx. what: 0 to remove, -1 to move fx up in chain, 1 to move fx down in chain.
## SNM_ReadMediaFileTag
```
boolean retval, string tagval = reaper.SNM_ReadMediaFileTag(string fn, string tag)
```

[S&M] Reads a media file tag. Supported tags: "artist", "album", "genre", "comment", "title", "track" (track number) or "year". Returns false if tag was not found. See SNM_TagMediaFile.
## SNM_RemoveReceive
```
boolean reaper.SNM_RemoveReceive(MediaTrack tr, integer rcvidx)
```

[S&M] Deprecated, see RemoveTrackSend (v5.15pre1+). Removes a receive. Returns false if nothing updated.
## SNM_RemoveReceivesFrom
```
boolean reaper.SNM_RemoveReceivesFrom(MediaTrack tr, MediaTrack srctr)
```

[S&M] Removes all receives from srctr. Returns false if nothing updated.
## SNM_SelectResourceBookmark
```
integer reaper.SNM_SelectResourceBookmark(string name)
```

[S&M] Select a bookmark of the Resources window. Returns the related bookmark id (or -1 if failed).
## SNM_SetDoubleConfigVar
```
boolean reaper.SNM_SetDoubleConfigVar(string varname, number newvalue)
```

[S&M] Sets a floating-point preference (look in project prefs first, then in general prefs). Returns false if failed (e.g. varname not found or newvalue out of range).
## SNM_SetDoubleConfigVarEx
```
boolean reaper.SNM_SetDoubleConfigVarEx(ReaProject proj, string varname, number newvalue)
```

[S&M] See SNM_SetDoubleConfigVar.
## SNM_SetFastString
```
WDL_FastString reaper.SNM_SetFastString(WDL_FastString str, string newstr)
```

[S&M] Sets the "fast string" content. Returns str for facility.
## SNM_SetIntConfigVar
```
boolean reaper.SNM_SetIntConfigVar(string varname, integer newvalue)
```

[S&M] Sets an integer preference (look in project prefs first, then in general prefs). Returns false if failed (e.g. varname not found or newvalue out of range).
## SNM_SetIntConfigVarEx
```
boolean reaper.SNM_SetIntConfigVarEx(ReaProject proj, string varname, integer newvalue)
```

[S&M] See SNM_SetIntConfigVar.
## SNM_SetLongConfigVar
```
boolean reaper.SNM_SetLongConfigVar(string varname, integer newHighValue, integer newLowValue)
```

[S&M] Sets a 64-bit integer preference from two 32-bit integers (look in project prefs first, then in general prefs). Returns false if failed (e.g. varname not found).
## SNM_SetLongConfigVarEx
```
boolean reaper.SNM_SetLongConfigVarEx(ReaProject proj, string varname, integer newHighValue, integer newLowValue)
```

[S&M] SNM_SetLongConfigVar.
## SNM_SetProjectMarker
```
boolean reaper.SNM_SetProjectMarker(ReaProject proj, integer num, boolean isrgn, number pos, number rgnend, string name, integer color)
```

[S&M] Deprecated, see SetProjectMarker4 -- Same function as SetProjectMarker3() except it can set empty names "".
## SNM_SetStringConfigVar
```
boolean reaper.SNM_SetStringConfigVar(string varname, string newvalue)
```

[S&M] Sets a string preference (general prefs only). Returns false if failed (e.g. varname not found or value too long). See get_config_var_string.
## SNM_TagMediaFile
```
boolean reaper.SNM_TagMediaFile(string fn, string tag, string tagval)
```

[S&M] Tags a media file thanks to TagLib. Supported tags: "artist", "album", "genre", "comment", "title", "track" (track number) or "year". Use an empty tagval to clear a tag. When a file is opened in REAPER, turn it offline before using this function. Returns false if nothing updated. See SNM_ReadMediaFileTag.
## SNM_TieResourceSlotActions
```
reaper.SNM_TieResourceSlotActions(integer bookmarkId)
```

[S&M] Attach Resources slot actions to a given bookmark.
## SN_FocusMIDIEditor
```
reaper.SN_FocusMIDIEditor()
```

Focuses the active/open MIDI editor.
## ULT_GetMediaItemNote
```
string reaper.ULT_GetMediaItemNote(MediaItem item)
```

[ULT] Deprecated, see GetSetMediaItemInfo_String (v5.95+). Get item notes.
## ULT_SetMediaItemNote
```
reaper.ULT_SetMediaItemNote(MediaItem item, string note)
```

[ULT] Deprecated, see GetSetMediaItemInfo_String (v5.95+). Set item notes.
## Xen_AudioWriter_Create
```
AudioWriter reaper.Xen_AudioWriter_Create(string filename, integer numchans, integer samplerate)
```

Creates writer for 32 bit floating point WAV
## Xen_AudioWriter_Destroy
```
reaper.Xen_AudioWriter_Destroy(AudioWriter writer)
```

Destroys writer
## Xen_AudioWriter_Write
```
integer reaper.Xen_AudioWriter_Write(AudioWriter writer, integer numframes, identifier data, integer offset)
```

Write interleaved audio data to disk
## Xen_GetMediaSourceSamples
```
integer reaper.Xen_GetMediaSourceSamples(PCM_source src, identifier destbuf, integer destbufoffset, integer numframes, integer numchans, number samplerate, number sourceposition)
```

Get interleaved audio data from media source
## Xen_StartSourcePreview
```
integer reaper.Xen_StartSourcePreview(PCM_source source, number gain, boolean loop, optional integer outputchanindexIn)
```

Start audio preview of a PCM_source. Returns id of a preview handle that can be provided to Xen_StopSourcePreview.
If the given PCM_source does not belong to an existing MediaItem/Take, it will be deleted by the preview system when the preview is stopped.
## Xen_StopSourcePreview
```
integer reaper.Xen_StopSourcePreview(integer preview_id)
```

Stop audio preview. id -1 stops all.
## lua_atexit
```
reaper.atexit(function)
```

Adds code to be executed when the script finishes or is ended by the user. Typically used to clean up after the user terminates defer() or runloop() code.
## lua_defer
```
reaper.defer(function)
```

Adds code to be called back by REAPER. Used to create persistent ReaScripts that continue to run and respond to input, while the user does other tasks. Identical to runloop().Note that no undo point will be automatically created when the script finishes, unless you create it explicitly.
## lua_get_action_context
```
reaper.get_action_context()
```

is_new_value,filename,sectionID,cmdID,mode,resolution,val,contextstr = reaper.get_action_context()Returns contextual information about the script, typically MIDI/OSC input values.val will be set to a relative or absolute value depending on mode (=0: absolute mode, >0: relative modes).resolution=127 for 7-bit resolution, =16383 for 14-bit resolution.sectionID, and cmdID will be set to -1 if the script is not part of the action list.mode, resolution and val will be set to -1 if the script was not triggered via MIDI/OSC.contextstr may be empty or one of:
## lua_gfx_variables
```
gfx VARIABLES
```

The following global variables are special and will be used by the graphics system:
## lua_gfx.arc
```
gfx.arc(x,y,r,ang1,ang2[,antialias])
```

Draws an arc of the circle centered at x,y, with ang1/ang2 being specified in radians.
## lua_gfx.blit
```
gfx.blit(source[, scale, rotation, srcx, srcy, srcw, srch, destx, desty, destw, desth, rotxoffs, rotyoffs])
```

Copies from source (-1 = main framebuffer, or an image from gfx.loadimg() etc), using current opacity and copy mode (set with gfx.a, gfx.mode).If destx/desty are not specified, gfx.x/gfx.y will be used as the destination position.scale (1.0 is unscaled) will be used only if destw/desth are not specified.rotation is an angle in radianssrcx/srcy/srcw/srch specify the source rectangle (if omitted srcw/srch default to image size)destx/desty/destw/desth specify destination rectangle (if not specified destw/desth default to srcw/srch * scale).
## lua_gfx.blitext
```
gfx.blitext(source,coordinatelist,rotation)
```

Deprecated, use gfx.blit instead.
## lua_gfx.blurto
```
gfx.blurto(x,y)
```

Blurs the region of the screen between gfx.x,gfx.y and x,y, and updates gfx.x,gfx.y to x,y.
## lua_gfx.circle
```
gfx.circle(x,y,r[,fill,antialias])
```

Draws a circle, optionally filling/antialiasing.
## lua_gfx.clienttoscreen
```
gfx.clienttoscreen(x,y)
```

Converts the coordinates x,y to screen coordinates, returns those values.
## lua_gfx.deltablit
```
gfx.deltablit(srcimg,srcs,srct,srcw,srch,destx,desty,destw,desth,dsdx,dtdx,dsdy,dtdy,dsdxdy,dtdxdy[,usecliprect=1])
```

Blits from srcimg(srcx,srcy,srcw,srch) to destination (destx,desty,destw,desth). Source texture coordinates are s/t, dsdx represents the change in s coordinate for each x pixel, dtdy represents the change in t coordinate for each y pixel, etc. dsdxdy represents the change in dsdx for each line. If usecliprect is specified and 0, then srcw/srch are ignored.
## lua_gfx.dock
```
gfx.dock(v[,wx,wy,ww,wh])
```

Call with v=-1 to query docked state, otherwise v>=0 to set docked state. State is &1 if docked, second byte is docker index (or last docker index if undocked). If wx-wh specified, additional values will be returned with the undocked window position/size
## lua_gfx.drawchar
```
gfx.drawchar(char)
```

Draws the character (can be a numeric ASCII code as well), to gfx.x, gfx.y, and moves gfx.x over by the size of the character.
## lua_gfx.drawnumber
```
gfx.drawnumber(n,ndigits)
```

Draws the number n with ndigits of precision to gfx.x, gfx.y, and updates gfx.x to the right side of the drawing. The text height is gfx.texth.
## lua_gfx.drawstr
```
gfx.drawstr("str"[,flags,right,bottom])
```

Draws a string at gfx.x, gfx.y, and updates gfx.x/gfx.y so that subsequent draws will occur in a similar place.
## lua_gfx.getchar
```
gfx.getchar([char, unichar])
```

If char is 0 or omitted, returns a character from the keyboard queue, or 0 if no character is available, or -1 if the graphics window is not open. If char is specified and nonzero, that character's status will be checked, and the function will return greater than 0 if it is pressed. Note that calling gfx.getchar() at least once causes gfx.mouse_cap to reflect keyboard modifiers even when the mouse is not captured.
## lua_gfx.getdropfile
```
gfx.getdropfile(idx)
```

Returns success,string for dropped file index idx. call gfx.dropfile(-1) to clear the list when finished.
## lua_gfx.getfont
```
gfx.getfont()
```

Returns current font index, and the actual font face used by this font (if available).
## lua_gfx.getimgdim
```
gfx.getimgdim(handle)
```

Retreives the dimensions of an image specified by handle, returns w, h pair.
## lua_gfx.getpixel
```
gfx.getpixel()
```

Returns r,g,b values [0..1] of the pixel at (gfx.x,gfx.y)
## lua_gfx.gradrect
```
gfx.gradrect(x,y,w,h, r,g,b,a[, drdx, dgdx, dbdx, dadx, drdy, dgdy, dbdy, dady])
```

Fills a gradient rectangle with the color and alpha specified. drdx-dadx reflect the adjustment (per-pixel) applied for each pixel moved to the right, drdy-dady are the adjustment applied for each pixel moved toward the bottom. Normally drdx=adjustamount/w, drdy=adjustamount/h, etc.
## lua_gfx.init
```
gfx.init("name"[,width,height,dockstate,xpos,ypos])
```

Initializes the graphics window with title name. Suggested width and height can be specified. If window is already open, a non-empty name will re-title window, or an empty title will resize window.
## lua_gfx.line
```
gfx.line(x,y,x2,y2[,aa])
```

Draws a line from x,y to x2,y2, and if aa is not specified or 0.5 or greater, it will be antialiased.
## lua_gfx.lineto
```
gfx.lineto(x,y[,aa])
```

Draws a line from gfx.x,gfx.y to x,y. If aa is 0.5 or greater, then antialiasing is used. Updates gfx.x and gfx.y to x,y.
## lua_gfx.loadimg
```
gfx.loadimg(image,"filename")
```

Load image from filename into slot 0..1024-1 specified by image. Returns the image index if success, otherwise -1 if failure. The image will be resized to the dimensions of the image file.
## lua_gfx.measurechar
```
gfx.measurechar(char)
```

Measures the drawing dimensions of a character with the current font (as set by gfx.setfont). Returns width and height of character.
## lua_gfx.measurestr
```
gfx.measurestr("str")
```

Measures the drawing dimensions of a string with the current font (as set by gfx.setfont). Returns width and height of string.
## lua_gfx.muladdrect
```
gfx.muladdrect(x,y,w,h,mul_r,mul_g,mul_b[,mul_a,add_r,add_g,add_b,add_a])
```

Multiplies each pixel by mul_* and adds add_*, and updates in-place. Useful for changing brightness/contrast, or other effects.
## lua_gfx.printf
```
gfx.printf("format"[, ...])
```

Formats and draws a string at gfx.x, gfx.y, and updates gfx.x/gfx.y accordingly (the latter only if the formatted string contains newline). For more information on format strings, see sprintf()
## lua_gfx.quit
```
gfx.quit()
```

Closes the graphics window.
## lua_gfx.rect
```
gfx.rect(x,y,w,h[,filled])
```

Fills a rectangle at x,y, w,h pixels in dimension, filled by default.
## lua_gfx.rectto
```
gfx.rectto(x,y)
```

Fills a rectangle from gfx.x,gfx.y to x,y. Updates gfx.x,gfx.y to x,y.
## lua_gfx.roundrect
```
gfx.roundrect(x,y,w,h,radius[,antialias])
```

Draws a rectangle with rounded corners.
## lua_gfx.screentoclient
```
gfx.screentoclient(x,y)
```

Converts the screen coordinates x,y to client coordinates, returns those values.
## lua_gfx.set
```
gfx.set(r[,g,b,a,mode,dest,a2])
```

Sets gfx.r/gfx.g/gfx.b/gfx.a/gfx.mode/gfx.a2, sets gfx.dest if final parameter specified
## lua_gfx.setcursor
```
gfx.setcursor(resource_id,custom_cursor_name)
```

Sets the mouse cursor to resource_id and/or custom_cursor_name.
## lua_gfx.setfont
```
gfx.setfont(idx[,"fontface", sz, flags])
```

Can select a font and optionally configure it. idx=0 for default bitmapped font, no configuration is possible for this font. idx=1..16 for a configurable font, specify fontface such as "Arial", sz of 8-100, and optionally specify flags, which is a multibyte character, which can include 'i' for italics, 'u' for underline, or 'b' for bold. These flags may or may not be supported depending on the font and OS. After calling gfx.setfont(), gfx.texth may be updated to reflect the new average line height.
## lua_gfx.setimgdim
```
gfx.setimgdim(image,w,h)
```

Resize image referenced by index 0..1024-1, width and height must be 0-8192. The contents of the image will be undefined after the resize.
## lua_gfx.setpixel
```
gfx.setpixel(r,g,b)
```

Writes a pixel of r,g,b to gfx.x,gfx.y.
## lua_gfx.showmenu
```
gfx.showmenu("str")
```

Shows a popup menu at gfx.x,gfx.y. str is a list of fields separated by | characters. Each field represents a menu item.Fields can start with special characters:
## lua_gfx.transformblit
```
gfx.transformblit(srcimg,destx,desty,destw,desth,div_w,div_h,table)
```

Blits to destination at (destx,desty), size (destw,desth). div_w and div_h should be 2..64, and table should point to a table of 2*div_w*div_h values (table can be a regular table or (for less overhead) a reaper.array). Each pair in the table represents a S,T coordinate in the source image, and the table is treated as a left-right, top-bottom list of texture coordinates, which will then be rendered to the destination.
## lua_gfx.triangle
```
gfx.triangle(x1,y1,x2,y2,x3,y3[x4,y4...])
```

Draws a filled triangle, or any convex polygon.
## lua_gfx.update
```
gfx.update()
```

Updates the graphics display, if opened
## lua_gmem_attach
```
reaper.gmem_attach(sharedMemoryName)
```

Causes gmem_read()/gmem_write() to read EEL2/JSFX/Video shared memory segment named by parameter. Set to empty string to detach. 6.20+: returns previous shared memory segment name.
## lua_gmem_read
```
reaper.gmem_read(index)
```

Read (number) value from shared memory attached-to by gmem_attach(). index can be [0..1<<25).
## lua_gmem_write
```
reaper.gmem_write(index,value)
```

Write (number) value to shared memory attached-to by gmem_attach(). index can be [0..1<<25).
## lua_new_array
```
reaper.new_array([table|array][size])
```

Creates a new reaper.array object of maximum and initial size size, if specified, or from the size/values of a table/array. Both size and table/array can be specified, the size parameter will override the table/array size.
## lua_runloop
```
reaper.runloop(function)
```

Adds code to be called back by REAPER. Used to create persistent ReaScripts that continue to run and respond to input, while the user does other tasks. Identical to defer().Note that no undo point will be automatically created when the script finishes, unless you create it explicitly.
## lua_set_action_options
```
reaper.set_action_options(flag)
```

reaper.set_action_options(flag)Sets action options for the script.flag&1: script will auto-terminate if re-launched while already runningflag&2: if (flag&1) is set, script will re-launch after auto-terminating. otherwise, re-launch is ignored.flag&4: set script toggle state onflag&8: set script toggle state off
## lua_{reaper.array}.clear
```
{reaper.array}.clear([value, offset, size])
```

Sets the value of zero or more items in the array. If value not specified, 0.0 is used. offset is 1-based, if size omitted then the maximum amount available will be set.
## lua_{reaper.array}.convolve
```
{reaper.array}.convolve([src, srcoffs, size, destoffs])
```

Convolves complex value pairs from reaper.array, starting at 1-based srcoffs, reading/writing to 1-based destoffs. size is in normal items (so it must be even)
## lua_{reaper.array}.copy
```
{reaper.array}.copy([src, srcoffs, size, destoffs])
```

Copies values from reaper.array or table, starting at 1-based srcoffs, writing to 1-based destoffs.
## lua_{reaper.array}.fft
```
{reaper.array}.fft(size[, permute, offset])
```

Performs a forward FFT of size. size must be a power of two between 4 and 32768 inclusive. If permute is specified and true, the values will be shuffled following the FFT to be in normal order.
## lua_{reaper.array}.fft_real
```
{reaper.array}.fft_real(size[, permute, offset])
```

Performs a forward real->complex FFT of size. size must be a power of two between 4 and 32768 inclusive. If permute is specified and true, the values will be shuffled following the FFT to be in normal order.
## lua_{reaper.array}.get_alloc
```
{reaper.array}.get_alloc()
```

Returns the maximum (allocated) size of the array.
## lua_{reaper.array}.ifft
```
{reaper.array}.ifft(size[, permute, offset])
```

Performs a backwards FFT of size. size must be a power of two between 4 and 32768 inclusive. If permute is specified and true, the values will be shuffled before the IFFT to be in fft-order.
## lua_{reaper.array}.ifft_real
```
{reaper.array}.ifft_real(size[, permute, offset])
```

Performs a backwards complex->real FFT of size. size must be a power of two between 4 and 32768 inclusive. If permute is specified and true, the values will be shuffled before the IFFT to be in fft-order.
## lua_{reaper.array}.multiply
```
{reaper.array}.multiply([src, srcoffs, size, destoffs])
```

Multiplies values from reaper.array, starting at 1-based srcoffs, reading/writing to 1-based destoffs.
## lua_{reaper.array}.resize
```
{reaper.array}.resize(size)
```

Resizes an array object to size. size must be [0..max_size].
## lua_{reaper.array}.table
```
{reaper.array}.table([offset, size])
```

Returns a new table with values from items in the array. Offset is 1-based and if size is omitted all available values are used.
