[![DOI](https://img.shields.io/badge/DOI-10.82901%2Fnemar.nm000370-blue)](https://doi.org/10.82901/nemar.nm000370)

Human intraoperative Neuropixels recordings, LF band (Paulk et al. 2022, DANDI 000397)
======================================================================================

Overview
--------
Recordings from a single Neuropixels 1.0 silicon probe (thick-shank variant, 384 recorded sites) inserted
into human cortex during neurosurgery at Massachusetts General Hospital. Three participants, one recording
each, without a task:
  Pt01  right dorsolateral prefrontal cortex, DBS lead implantation (movement disorder), general anesthesia
  Pt02  left dorsolateral prefrontal cortex, DBS lead implantation (movement disorder), awake with monitored
        anesthesia care
  Pt03  left anterior temporal lobe cortex, anterior temporal lobectomy (epilepsy), general anesthesia
These are the three successful recordings of the article; six further attempts (probe fracture or excessive
noise) are described in the article but not released.

Scope note: Neuropixels are penetrating high-density silicon probes, not clinical iEEG electrodes. This
dataset contains only the local-field-potential (LF) band (0.5-500 Hz, 2.5 kHz), which is iEEG-like and is
represented here in iEEG-BIDS ("iEEG-adjacent"). The 30 kHz action-potential (AP) band is not converted; it
remains, unchanged, in the original NWB files under sourcedata/dandi-000397/.

Sources:
  Paulk AC et al. Large-scale neural recordings with single neuron resolution using Neuropixels probes in
  human cortex. Nature Neuroscience 25, 252-263 (2022). https://doi.org/10.1038/s41593-021-00997-0
  Dryad: doi:10.5061/dryad.d2547d840 (CC0; original SpikeGLX .bin/.meta files of the AP and LF bands,
  motion-corrected AP data and more, about 137 GB).
  DANDI 000397 (CC0): NWB conversion of the raw AP and LF bands (NeuroConv). At conversion time (2026-10-06)
  the Dandiset had no published version; the 3 NWB assets were downloaded from the draft and verified against
  the DANDI SHA-256 digests (sourcedata/sourcedata_provenance.json).
Please cite the article and the data records.

Ethics
------
From the Dryad release methods: "All patients voluntarily participated after informed consent according to
guidelines as monitored by the Massachusetts General Brigham (previously Partners) Institutional Review
Board (IRB) Massachusetts General Hospital (MGH). Participants were informed that participation in the
experiment would not alter their clinical treatment in any way, and that they could withdraw at any time
without jeopardizing their clinical care. Participants were not compensated monetarily for participating."
The data are released under CC0.

Contents
--------
3 participants, 3 recordings (one each), 384 LF-band channels per recording at 2500 Hz: Pt01 833.8 s,
Pt02 873.3 s, Pt03 586.3 s (38.2 min in total). About 4.4 GB of BrainVision data plus 24.1 GB of original NWB
(LF + AP bands) in sourcedata/.

  sub-Pt0X/ieeg/*_ieeg.vhdr/.vmrk/.eeg  BrainVision, INT_16, resolution 4.6875 µV per bit (the NWB conversion).
  sub-Pt0X/ieeg/*_channels.tsv          384 probe sites in source order (LF0 ... LF383).
  sub-Pt0X/ieeg/*_electrodes.tsv        probe-relative site positions (no anatomical coordinates).
  sub-Pt0X/sub-Pt0X_scans.tsv           source file, SHA-256 and series.
  sourcedata/dandi-000397/              byte-identical copies of the three DANDI NWB files (LF and AP bands).

Signal: what was converted and how
----------------------------------
Source: acquisition/ElectricalSeriesLFP of each NWB file ("LFP traces for the processed (lf) SpikeGLX data"):
int16, conversion 4.6875e-06 V per bit, offset 0, 2500 Hz from 0 s, 384 channels. The BrainVision .eeg files
contain exactly these int16 samples (multiplexed, little-endian) with resolution 4.6875 µV, so the conversion
is lossless; nothing was filtered, resampled, re-referenced, cropped, or removed.
Acquisition (Dryad methods): SpikeGLX Release v20201103-phase30; LF band band-pass filtered 0.5-500 Hz and
sampled at 2.5 kHz; AP band 0.3-10 kHz at 30 kHz; 10-bit ADC with a 10 mVpp linear range; default electrode map
(the 384 most distal sites, lower third of the shank). Reference and ground: sterile needle electrodes
(Medtronic) in nearby muscle, often scalp. Channel inter-sample shifts of the Neuropixels ADC multiplexing are
listed in channels.tsv (inter_sample_shift) and are not corrected in the data. The recordings contain movement
artefacts (the authors provide motion-corrected AP-band data on Dryad).
Channel names: the NWB electrodes table names its rows after the AP band (AP0 ... AP383); the same rows carry
the LF band, so the LF channels are named LF0 ... LF383 here (source name in channels.tsv).
Channel type: BIDS has no channel type for silicon-probe sites; SEEG (intracortical depth recording) is used.

Electrodes and coordinates
--------------------------
No anatomical coordinates are released. electrodes.tsv has x, y, z = n/a and gives the site position on the
probe (probe_x_um across the shank, probe_y_um along the shank), contact shape and site number from the NWB
electrodes table, and the recorded area from the Dryad methods. The NWB device description reads
{"probe_type": "0", "probe_type_description": "NP1.0", "flex_part_number": "NP2_FLEX_0",
"connected_base_station_part_number": "NP2_QBSC_00"}.

Participants
------------
Age and sex are not released per participant (NWB age is the cohort range P34Y/P75Y and sex "U"; the full
cohort of 9 had a mean age of 59 years, range 34-75, 7 female). participants.tsv gives age and sex as n/a,
the cohort age range verbatim, anesthesia state, procedure and recorded area.
Cohort (Dryad methods; Paulk et al. 2022 Supplementary Table 1): 9 participants at Massachusetts General
Hospital already scheduled for a craniotomy: 1 left anterior frontal tumour removal (thin probe, fractured, no
recording), 6 deep brain stimulation lead implantations (1 thin probe fractured; 3 thick-probe recordings with
considerable noise; Pt. 01 and Pt. 02 released) and 2 left anterior temporal lobectomies for epilepsy (1 with
considerable noise; Pt. 03 released). Supplementary Table 1 labels the released recordings "Pt. 01" to "Pt. 03"
with procedure, anesthesia state and location identical to the Dryad methods, which proves the mapping to
sub-Pt01 ... sub-Pt03. participants.tsv adds from that table the probe variant (thick for all three) and the
spike-sorting yield (total clusters, single units, MUA clusters: Pt01 262/202/60, Pt02 312/178/134,
Pt03 29/19/10); the spike-sorted units themselves are not part of this release.
Not available from any source checked (n/a): per-participant age and sex, handedness, diagnosis details beyond
the procedure, and the recording year (NWB session_start_time is the placeholder 1900-01-01; the Dryad methods and the
article supplement give no dates; the original SpikeGLX .meta files on Dryad could not be downloaded anonymously).

Events
------
None: the recordings have no task and the NWB files contain no event or trial tables.

Conversion checks
-----------------
- For every recording the int16 samples in the .eeg file were compared with the NWB dataset for all samples:
  identical; file size equals samples x channels x 2 bytes.
- MNE-Python reads every file with the right sampling rate, 384 channels and sample count; start, middle and
  end windows equal the NWB int16 values times the NWB conversion (in volts).
- The NWB copies in sourcedata/ match the DANDI SHA-256 digests.
- bids-validator 3.0.2: 0 errors; warnings for recommended fields the source does not document and for the
  absence of events files (there are no events).

Conversion code: b2dandi_npx_bids.py (iEEG-NEMAR campaign, batch 2), using h5py; checked with MNE-Python.

Known caveats
-------------
- LF band only; the 30 kHz AP band stays in the NWB files under sourcedata/ (see Scope note).
- No anatomical coordinates; channel inter-sample shifts are not corrected; recordings contain movement
  artefacts (see Signal and Electrodes and coordinates).
- Per-participant age, sex and recording year are not released.

How to load
-----------
  from mne_bids import BIDSPath, read_raw_bids
  bp = BIDSPath(root="nm000370", subject="Pt01", task="intraop", datatype="ieeg")
  raw = read_raw_bids(bp)            # 384 LF-band channels at 2500 Hz

Citation
--------
Paulk AC, Kfir Y, Khanna AR, Mustroph ML, Trautmann EM, Soper DJ, Stavisky SD, Welkenhuysen M, Dutta B,
Shenoy KV, Hochberg LR, Richardson RM, Williams ZM, Cash SS. Large-scale neural recordings with single neuron
resolution using Neuropixels probes in human cortex. Nature Neuroscience 25, 252-263 (2022).
doi:10.1038/s41593-021-00997-0 ; data: Dryad doi:10.5061/dryad.d2547d840 and DANDI:000397.

Provenance of the 2026-10-07 metadata enrichment
------------------------------------------------
Paulk et al. 2022 Supplementary Information (Supplementary Table 1, freely downloadable; the article body is
subscription-only and was not read); Dryad record doi:10.5061/dryad.d2547d840 (methods, API metadata).
