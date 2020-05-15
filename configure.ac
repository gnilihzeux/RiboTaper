dnl -*- Autoconf -*-

AC_INIT(RiboTaper, 1.3.1a)
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_MACRO_DIR([m4])
AM_INIT_AUTOMAKE([color-tests -Wall -Wno-portability foreign])
AM_SILENT_RULES([yes])

# Check for any variant of "awk" and store path in "AWK" variable
AC_PROG_AWK
AC_PROG_SED

AC_ARG_VAR(GNUBASH, override location of "bash" executable)
AC_ARG_VAR(SAMTOOLS, override location of "samtools" executable)
AC_ARG_VAR(BEDTOOLS, override location of "bedtools" executable)
AC_ARG_VAR(COVERAGE_BED, override location of "coverageBed" executable)
AC_ARG_VAR(BAM_TO_BED, override location of "bamToBed" executable)
AC_ARG_VAR(CLOSEST_BED, override location of "closestBed" executable)
AC_ARG_VAR(WINDOW_BED, override location of "windowBed" executable)
AC_ARG_VAR(INTERSECT_BED, override location of "intersectBed" executable)
AC_ARG_VAR(FASTA_FROM_BED, override location of "fastaFromBed" executable)
AC_ARG_VAR(RSCRIPT, override location of "Rscript" executable)
AC_ARG_VAR(R, override location of "R" executable)

# Check for required programmes and store their full path in the given
# variables.  The variables are used to substitute placeholders in the
# scripts.
AS_IF([test -z "$GNUBASH"],
      [AC_PATH_PROG([GNUBASH], [bash])],
      [AC_MSG_NOTICE([Using $GNUBASH as bash executable.])])

AS_IF([test -z "$BEDTOOLS"],
      [AC_PATH_PROG([BEDTOOLS], [bedtools])],
      [AC_MSG_NOTICE([Using $BEDTOOLS as bedtools executable.])])
BEDTOOLS_VERSION_MAX=2.18.0
BEDTOOLS_VERSION=$($BEDTOOLS --version | $SED 's/^bedtools v//')
AX_COMPARE_VERSION([$BEDTOOLS_VERSION], [gt], [$BEDTOOLS_VERSION_MAX],
      [AC_MSG_ERROR([The output format of your version of bedtools is not compatible with what Ribotaper expects.  Please install Bedtools $BEDTOOLS_VERSION_MAX or lower.])])

AS_IF([test -z "$COVERAGE_BED"],
      [AC_PATH_PROG([COVERAGE_BED], [coverageBed])],
      [AC_MSG_NOTICE([Using $COVERAGE_BED as coverageBed executable.])])
AS_IF([test -z "$BAM_TO_BED"],
      [AC_PATH_PROG([BAM_TO_BED], [bamToBed])],
      [AC_MSG_NOTICE([Using $BAM_TO_BED as bamToBed executable.])])
AS_IF([test -z "$CLOSEST_BED"],
      [AC_PATH_PROG([CLOSEST_BED], [closestBed])],
      [AC_MSG_NOTICE([Using $CLOSEST_BED as closestBed executable.])])
AS_IF([test -z "$WINDOW_BED"],
      [AC_PATH_PROG([WINDOW_BED], [windowBed])],
      [AC_MSG_NOTICE([Using $WINDOW_BED as windowBed executable.])])
AS_IF([test -z "$INTERSECT_BED"],
      [AC_PATH_PROG([INTERSECT_BED], [intersectBed])],
      [AC_MSG_NOTICE([Using $INTERSECT_BED as intersectBed executable.])])
AS_IF([test -z "$FASTA_FROM_BED"],
      [AC_PATH_PROG([FASTA_FROM_BED], [fastaFromBed])],
      [AC_MSG_NOTICE([Using $FASTA_FROM_BED as fastaFromBed executable.])])
AS_IF([test -z "$SAMTOOLS"],
      [AC_PATH_PROG([SAMTOOLS], [samtools])],
      [AC_MSG_NOTICE([Using $SAMTOOLS as samtools executable.])])
AS_IF([test -z "$RSCRIPT"],
      [AC_PATH_PROG([RSCRIPT], [Rscript])],
      [AC_MSG_NOTICE([Using $RSCRIPT as Rscript executable.])])
AS_IF([test -z "$R"],
      [AC_PATH_PROG([R], [R])],
      [AC_MSG_NOTICE([Using $R as R executable.])])

AC_DEFUN([AX_TEST_R_PACKAGE], [
    pushdef([PKG],$1)
    AC_MSG_CHECKING([for R package "PKG"])
    if test -z "$HURRY"
    then
      TEST=$($R --silent --vanilla -e 'if(!require("PKG")) stop("not found")' 2>/dev/null)
      AS_IF([test $? != 0],
            [AC_MSG_ERROR([R package PKG could not be loaded])],
            [AC_MSG_RESULT([OK])])
    else
      AC_MSG_RESULT([OK])
    fi
    popdef([PKG])
])

if test "x$R" == x
then
  AC_MSG_ERROR([R could not be found, so we cannot test for R packages.])
else
  AX_TEST_R_PACKAGE([XNomial])
  AX_TEST_R_PACKAGE([foreach])
  AX_TEST_R_PACKAGE([doMC])
  AX_TEST_R_PACKAGE([multitaper])
  AX_TEST_R_PACKAGE([seqinr])
fi

# Substitute placeholders to generate these target files
AC_CONFIG_FILES([Makefile
                 scripts/P_sites_RNA_sites_calc.bash
                 scripts/create_metaplots_nodo.bash
                 scripts/analyze_multi_clust.bash
                 scripts/create_tracks.bash
                 scripts/tracks_analysis.R.in
                 scripts/metag.R
                 scripts/gtf_to_start_stop_tr.R
                 scripts/genes_coor.R
                 scripts/quality_check.R
                 scripts/NONCCDS_orf_finder.R.in
                 scripts/annotate_exons.R.in
                 scripts/create_protein_db.R
                 scripts/ORF_final_results.R
                 scripts/write_startstops.R
                 scripts/include_multi_nomerge.R
                 scripts/CCDS_orf_finder.R.in])

AC_CONFIG_FILES([scripts/Ribotaper.sh.in], [chmod +x scripts/Ribotaper.sh.in])
AC_CONFIG_FILES([scripts/Ribotaper_ORF_find.sh.in], [chmod +x scripts/Ribotaper_ORF_find.sh.in])
AC_CONFIG_FILES([scripts/create_annotations_files.bash.in], [chmod +x scripts/create_annotations_files.bash.in])
AC_CONFIG_FILES([scripts/create_metaplots.bash.in], [chmod +x scripts/create_metaplots.bash.in])

AC_OUTPUT
