AutoDraft example
=================

One latex file, one makefile - instantly be able to build in either
draft or final mode from the command line.

Usage:
	make [all]
		- Will make the final version, if the source files are newer
		than the last build of any kind.
	make draft
		- Makes the file in draft mode. The example file also makes use
		of the _ifdraft_ package for extra draft functionality, such as
		the bounding boxes
	make final
		- Like all, but forces the recreation of the final version

