basler-objs = BaslerCamera.o BaslerInterface.o BaslerDetInfoCtrlObj.o BaslerSyncCtrlObj.o BaslerRoiCtrlObj.o BaslerBinCtrlObj.o

SRCS = $(basler-objs:.o=.cpp)

ifndef PYLON_ROOT
PYLON_ROOT = /opt/pylon
endif

ifndef GENICAM_ROOT_V2_1
GENICAM_ROOT_V2_1 = $(PYLON_ROOT)/genicam
endif

CXXFLAGS += -I../include -I../../../hardware/include -I../../../common/include \
			-I$(PYLON_ROOT)/include \
			-I$(GENICAM_ROOT_V2_1)/library/CPP/include \
			-DUSE_GIGE -Wall -pthread -fPIC -g

all:	Basler.o

Basler.o:	$(basler-objs)
	$(LD) -o $@ -r $+

clean:
	rm -f *.o *.P

%.o : %.cpp
	$(COMPILE.cpp) -MD $(CXXFLAGS) -o $@ $<
	@cp $*.d $*.P; \
	sed -e 's/#.*//' -e 's/^[^:]*: *//' -e 's/ *\\$$//' \
	-e '/^$$/ d' -e 's/$$/ :/' < $*.d >> $*.P; \
	rm -f $*.d


-include $(SRCS:.cpp=.P)



.PHONY: check-syntax
check-syntax:
	$(CXX) -Wall -Wextra -fsyntax-only $(CXXFLAGS) $(CHK_SOURCES)
