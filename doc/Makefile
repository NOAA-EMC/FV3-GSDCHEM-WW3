LOCAL_DOCS=$(wildcard *.md) $(wildcard *.dox)
CONTROL_FILES=Makefile prep_inputs.py Doxyfile.IN DoxygenLayout.xml.IN

TARGET=strahan@emcrzdm:/home/www/emc/htdocs/projects/nems-sample-v4

# Find Doxygen

ifndef DOXYGEN
DOXYGEN=doxygen
endif

ifeq ("$(DOXYGEN)","doxygen")
  THEIA_DOXYGEN=/scratch3/NCEPDEV/hwrf/save/Samuel.Trahan/doxygen-1.8.10/bin/doxygen
  JET_DOXYGEN=/contrib/doxygen/1.8.10/bin/doxygen
  LUNA_DOXYGEN=/gpfs/hps/emc/hwrf/noscrub/soft/doxygen-1.8.10/bin/doxygen
  TIDE_DOXYGEN=/hwrf/noscrub/soft/doxygen-1.8.10/bin/doxygen

  ifneq ($(wildcard $(THEIA_DOXYGEN)*),)
    DOXYGEN=$(THEIA_DOXYGEN)
  endif

  ifneq ($(wildcard $(JET_DOXYGEN)*),)
    DOXYGEN=$(JET_DOXYGEN)
  endif

  ifneq ($(wildcard $(LUNA_DOXYGEN)*),)
    DOXYGEN=$(LUNA_DOXYGEN)
  endif

  ifneq ($(wildcard $(TIDE_DOXYGEN)*),)
    DOXYGEN=$(TIDE_DOXYGEN)
  endif
endif

default:
	@echo Specify build mode:
	@echo doc        = build documentation just for this directory
	@echo nems-doc   = build full documentation website, including all apps
	@echo clean      = delete outputs
	@echo deliver    = copy to website
	exit 19

clean:
	rm -rf html webpage.tar.gz repo_info.sh.inc Doxyfile DoxygenLayout.xml

nems-doc:
	echo "Oopes!  Sam has not implemented this yet."

doc: clean
	./prep_inputs.py ..
	set -x ; $(DOXYGEN)
	tar -cpzf webpage.tar.gz html Doxyfile

deliver: html
	cd html && rsync -arv . "$(TARGET)/."

