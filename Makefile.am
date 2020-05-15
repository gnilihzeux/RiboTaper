# Copyright (C) 2016  Ricardo Wurmus <rekado@elephly.net>
#
# This file is part of RiboTaper.
# RiboTaper is a method for defining traslated ORFs using
# Ribosome Profiling data.
#
# RiboTaper is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# RiboTaper is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with RiboTaper.  If not, see <http://www.gnu.org/licenses/>.
#
# Contact: Lorenzo.Calviello@mdc-berlin.de
#######################################################################

ACLOCAL_AMFLAGS = -I m4

nodist_bin_SCRIPTS =				\
  scripts/create_annotations_files.bash		\
  scripts/create_metaplots.bash			\
  scripts/Ribotaper.sh				\
  scripts/Ribotaper_ORF_find.sh

dist_libexec_SCRIPTS =				\
  scripts/functions.R

nodist_libexec_SCRIPTS =			\
  scripts/config.bash				\
  scripts/P_sites_RNA_sites_calc.bash		\
  scripts/create_metaplots_nodo.bash		\
  scripts/analyze_multi_clust.bash		\
  scripts/create_tracks.bash			\
  scripts/metag.R				\
  scripts/gtf_to_start_stop_tr.R		\
  scripts/genes_coor.R				\
  scripts/quality_check.R			\
  scripts/create_protein_db.R			\
  scripts/ORF_final_results.R			\
  scripts/write_startstops.R			\
  scripts/include_multi_nomerge.R		\
  scripts/annotate_exons.R			\
  scripts/tracks_analysis.R			\
  scripts/NONCCDS_orf_finder.R			\
  scripts/CCDS_orf_finder.R

dist_doc_DATA =					\
  README

# This is a hack to let the main scripts know where to find the config
# files.
scripts/Ribotaper.sh: scripts/Ribotaper.sh.in
	sed -e "s|#:MAKE|\nlibexecdir=\"$(libexecdir)\"|" -i $<
	mv $< $@

scripts/Ribotaper_ORF_find.sh: scripts/Ribotaper_ORF_find.sh.in
	sed -e "s|#:MAKE|\nlibexecdir=\"$(libexecdir)\"|" -i $<
	mv $< $@

scripts/create_metaplots.bash: scripts/create_metaplots.bash.in
	sed -e "s|#:MAKE|\nlibexecdir=\"$(libexecdir)\"|" -i $<
	mv $< $@

scripts/create_annotations_files.bash: scripts/create_annotations_files.bash.in
	sed -e "s|#:MAKE|\nlibexecdir=\"$(libexecdir)\"|" -i $<
	mv $< $@

scripts/tracks_analysis.R: scripts/tracks_analysis.R.in
	sed -e "s|#:MAKE|\nlibexecdir <- \"$(libexecdir)\"|" -i $<
	mv $< $@

scripts/CCDS_orf_finder.R: scripts/CCDS_orf_finder.R.in
	sed -e "s|#:MAKE|\nlibexecdir <- \"$(libexecdir)\"|" -i $<
	mv $< $@

scripts/NONCCDS_orf_finder.R: scripts/NONCCDS_orf_finder.R.in
	sed -e "s|#:MAKE|\nlibexecdir <- \"$(libexecdir)\"|" -i $<
	mv $< $@

scripts/annotate_exons.R: scripts/annotate_exons.R.in
	sed -e "s|#:MAKE|\nlibexecdir <- \"$(libexecdir)\"|" -i $<
	mv $< $@

# This is a hack to configure some variables shared by all bash scripts.
scripts/config.bash:
	echo "export libexecdir=\"$(libexecdir)\"" > $@


all-local:
	@echo -e "\n\nRiboTaper has successfully been built."

install: install-am
	@echo -e "\n\nRiboTaper has successfully been installed."

CLEANFILES = \
  scripts/Ribotaper.sh \
  scripts/Ribotaper_ORF_find.sh \
  scripts/config.bash \
  scripts/annotate_exons.R \
  scripts/NONCCDS_orf_finder.R \
  scripts/CCDS_orf_finder.R \
  scripts/tracks_analysis.R \
  scripts/create_annotations_files.bash \
  scripts/create_metaplots.bash
