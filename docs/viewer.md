# Viewer

This chapter provides an overview of the main user interface for BrICS. We'll go over how to open a study, view different images within the study, and what the different buttons in the UI represent.

## Lexicon

Within BrICS, we try to use lexicon from the DICOM standard for medical imaging to describe patients, studies, and series. Below is a quick flowchart of the object hierarchy in BrICS.

```mermaid
graph TB
A(Project) --> B(Subject)
B --> C(Study)
C --> D(Series)
C --> E(Structure)
```
### Project
A project is the top-level object in the hierarchy, and represents a group of subjects who are to be analyzed together. It can be all the subjects within a clinical study, for example, or all the subjects for a particular analysis that you are trying to do. The Project level is also where authentication occurs for users; users are assigned to specific Projects, and if they don't have access to a Project, they  cannot access any of the data within that project.

A Project also consists of several settings (see the chapter on Administration), which are applied to all objects within the Project.
> Internally, a project ID is attached to every object stored in the database. This allows the software to quickly determine which Project settings to use.

### Subject

A Subject represents a subject (whether a volunteer, patient, a phantom, or an artificial data set). Every Subject in a Project must have a unique **subject_id**, which is an alpha-numeric string; it should not contain any PHI.

### Study
The main working unit of BrICS is the Study. A Study represents a set of images acquired (or generated) for a Subject that are meant to be considered concurrently for visualization or analysis.

In the standard DICOM lexicon, a study corresponds to a specific imaging session. For clinical MRI, a study often consists of multiple sequences (known as series) that are performed while the subject is in the scanner. A study in DICOM is always performed in one session. As such, it only contains one imaging modality (e.g. MRI or CT, but not both).

In BrICS, we expand the definition of Study to allow for series that are taken during different imaging sessions This can mean the same imaging modality from different dates/times, or different modalities. We do this because often we want to compare spectroscopic MRI data alongside other imaging modalities. Sometimes, these other modalities may be acquired at a different time or date. While technically a Study could include series from any date, it is generally good practice to group series in a Study if they should be considered together. An example: a patient undergoes the sMRI scan on January 1st, but no contrast-enhanced imaging was done at that time; the contrast-enhanced scan was performed on January 4th, but should be considered part of the same analysis. However, if the contrast-enhanced scan was done on February 1st, then it really should be part of a different Study.

#### UID

Similar to DICOM, every Study is identified by a [universally unique identifier](https://en.wikipedia.org/wiki/Universally_unique_identifier), a long period-separated numeric string.

#### Reference Series
Every Study contains one series which is considered to be the reference series. This is typically a high-resolution structure MRI, e.g. T1w MRI. All other series in this Study will be registered and aligned to this study. This allows voxel-to-voxel comparison of series within the same study, and allows Structures to be generated / visualized for all series in the study.

### Series

A series is a 3D image, either acquired directly from the scanner 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc0NTA4Mjg5NywtNTI1Nzg3OTk1LDU1Nj
Y5NDQ0NF19
-->