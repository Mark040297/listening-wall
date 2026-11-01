# Codebook: privacy-relevant capabilities of Intelligent Noise Control Systems (INCS)

Version 1 (before pilot). Version 2 changes are listed at the end.

Unit of coding: one record (a research article or a patent). Code what the record describes for its **own proposed or tested system**. Do not code systems that the record only cites as background.

Evidence: articles are coded from the title, abstract, and full text. Patents are coded from the title and abstract of the search record (`data/corpus/patents_included.csv`).

| No. | Variable | Values | Rule |
|---|---|---|---|
| 1 | `id` | text | RA1 to RA260 for articles; the patent identifier in `patents_included.csv` for patents. |
| 2 | `year` | 2015 to 2025 | Publication year (articles) or application year (patents), taken from the source file. Not a judgment. |
| 3 | `continuous_sensing` | yes / no / unclear | **yes**: the microphone runs whenever the system is active. This includes all feedforward and feedback ANC, adaptive filtering, and continuous monitoring. **no**: sensing is only on demand, by trigger, or duty cycled with the microphone off. **unclear**: the record gives no basis to tell. |
| 4 | `ai_ml` | yes / no / unclear | **yes**: the system uses a learned model (neural network, deep learning, machine learning classifier, fuzzy-neural system, reinforcement learning). **no**: the method is described and uses no learned model. Classical adaptive filters such as LMS, FxLMS, NLMS, and RLS are **no**. **unclear**: the method is not described. |
| 5 | `network` | yes / no / unclear | **yes**: the system sends or receives data to or from another device, a server, or a network (wireless, Bluetooth, Wi-Fi, IoT, cellular, cloud). Wired links inside one device do not count. **no**: the system is clearly standalone. **unclear**: not stated. |
| 6 | `sound_classification` | yes / no | **yes**: the system labels sound sources, events, or speech, including voice activity detection. Noise level estimation alone is **no**. |
| 7 | `speech_classification` | yes / no | **yes** if the labels in variable 6 include speech or voice. |
| 8 | `processing_location` | local_only / cloud_only / hybrid / not_specified | Where audio or audio features are processed. **cloud** means a remote server or cloud service. |
| 9 | `processing_domain` | time_domain / frequency_domain / time_frequency / unclear | Main signal domain of the core algorithm. Subband, FFT based, and STFT methods are frequency or time-frequency. |
| 10 | `deployment_setting` | building_interior / building_exterior / vehicle_interior / personal_wearable / residential_home / outdoor_urban / outdoor_industrial / laboratory_only / not_specified | Intended place of operation. **laboratory_only** (articles only) is used when the work is only simulation or lab testing **and** names no target setting. Aircraft, train, and ship cabins count as vehicle_interior. Headphones, earbuds, hearing aids, and helmets count as personal_wearable. Ducts, HVAC, rooms, and offices count as building_interior. |

Binary indicators used in the paper:

- continuous sensing = `continuous_sensing` is yes
- AI or ML = `ai_ml` is yes
- network = `network` is yes
- sound classification = `sound_classification` is yes
- cloud processing = `processing_location` is cloud_only or hybrid
- frequency domain processing = `processing_domain` is frequency_domain or time_frequency

Cleaning of the coder 1 sheets before publication (every changed cell is listed in `data/corpus/coder1_cleaning_log.csv` with its original value):

- R1: continuous sensing `adaptive` is recorded as yes (an adaptive ANC microphone runs continuously)
- R2: processing domain `not_specified` is recorded as unclear (one category in this codebook)
- R3: setting `headphones` is recorded as personal_wearable; R4: other setting labels outside the list are recorded as other
- R5: patent processing location cells that repeated the deployment setting label are recorded as not_specified (47 patents)
- R6: one article that coder 1 could not open (RA33) is recorded as not_coded and left out of the reliability comparison
- R7: patent year is the application year of the search record; R8: one column name spelling (DEPLOYMENT_SETTING)

Speech classification of patents was added by coder 1 after the main round (see `docs/coding_procedure.md`). It is not part of the cleaning log because it is a new code, not a cleaned one.

## Version 2 (after the pilot round of 15 articles and 15 patents)

The pilot was coded blind with version 1 and then compared with coder 1. The rules below were clarified before the main round. No rule was changed to copy a coder 1 value; each change makes a judgment rule explicit.

1. **processing_domain.** Code frequency_domain or time_frequency only when the core algorithm operates on a spectral representation (FFT, subband filter bank, STFT, frequency domain adaptive filter, frequency dependent control coefficients, band-wise control). A mention of a frequency range, a frequency band of interest, or a cut off frequency alone does not count. If the algorithm is not described, code unclear.
2. **ai_ml.** Statistical estimation methods (ICA, IVA, Gaussian mixture models used for blind source separation, Kalman filters), kernel adaptive filters, and optimization methods such as genetic algorithms are **no**, unless the authors call them machine learning or train a model on a data set.
3. **processing_location.** If the authors name a cloud server as a host for part of the processing, code hybrid, and code network as yes.
4. **deployment_setting.** Test noise recordings (for example car or fan noise) and applications listed only in the literature review do not set the deployment setting. Construction sites count as outdoor_industrial. Roadsides, streets, vertiports, and transport stations count as outdoor_urban.
5. **continuous_sensing.** Any ANC system with a microphone, hearing aids, and monitoring systems are yes even when the text does not say "continuous", because the method needs a live microphone signal. Use unclear when no microphone is described or the system type cannot be identified. Offline processing of stored recordings is unclear.
6. **network (patents).** A standalone device with no communication described is no. Coder 1 used unclear in this case; both map to "not present" in the binary indicator.
7. **sound_classification.** Speech enhancement or denoising alone is not classification. Selecting or generating control filters by noise type (SFANC, GFANC) is classification.

Pilot items are excluded from the reliability estimate. They were recoded with version 2 after the main round for completeness (not blind).

## Conventions fixed during the main round

Coder 2 fixed these conventions during the main round, when a case was not covered by version 2. Each one was applied to all later records and checked against earlier ones. They refine version 2 and do not change any of its rules.

1. Industrial machinery, factories, construction sites, power transformers, substations and power plants: outdoor_industrial, even when the authors mention nearby housing.
2. Windows, rooms, ducts, offices and office partitions: building_interior. Exterior facade speakers: building_exterior.
3. Aircraft, train, tractor, ambulance and car cabins: vehicle_interior.
4. Selective or generative fixed-filter ANC (SFANC, GFANC) with the CNN placed on a co-processor named as a separate device such as a mobile phone: network yes, because noise frames and filter weights pass between devices. If no device is named: unclear.
5. Swarm and evolutionary optimisers (artificial bee colony, cuckoo search, bat algorithm, genetic algorithm) used to update filter weights: ai_ml no.
6. Passive structures with no microphone in the proposed system (for example metamaterials): continuous_sensing unclear; microphones used only for study measurements do not count.
7. Drones and other systems the authors place in urban environments in their conclusions: outdoor_urban.
8. True wireless (Bluetooth) earbuds: network yes.
9. Communication devices whose microphone runs only during a user-started call, conference or push-to-talk press: continuous_sensing no. Applied to RA106, RA109 and RA197 (RA106 was revised from yes when the rule was fixed at RA197).
10. Voice call, teleconference, radio and speech coding systems: network yes, because the audio is sent to another party.
11. Handheld or body-carried personal devices without another category (two-way radios, mobile phones): personal_wearable.
12. Functional link artificial neural networks (FLANN) and their variants: ai_ml yes, because the authors call them neural networks.
13. Machine learning classes that are only loudness or intensity levels: sound_classification no, by the noise-level rule.
14. Windows and rooms that the authors place in homes, apartments, or dormitories: residential_home. Other windows: building_interior.
15. Systems for which the authors name several different target settings with equal weight: not_specified.
