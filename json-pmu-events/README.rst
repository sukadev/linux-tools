
csv2json
=========

Use ``csv2json`` to convert the CSV file from HW team to a set of JSON files.

	* Download *p9events.csv* to current directory
	* Make a directory *new-pmu-events/*
	* Run the script **csv2json** - this generates the JSON files in
	  *new-pmu-events/*

**NOTE**: Creates/overwrites log file *log-csv2json* as well as any ``.json``
files in *new-pmu-events/*

cmp-json-dirs
=============

Use ``cmp-json-dirs`` to summarize differences between two directories of
JSON files (eg: the JSON files from main line and new-pmu-events/ from above)

	* Run ``csv2json`` as described above to create *new-pmu-events/*
	* Make a directory *mainline/* and populate with the JSON files in
	  current mainline (i.e *tools/perf/pmu-events/arch/powerpc/power9/*)
	* Run ``./cmp-json-dirs mainline new-pmu-events`` for a summary of
	  differences (printed to ``stdout``).

TODO
=====
	Fix hardcoded file/directory names in the scripts
