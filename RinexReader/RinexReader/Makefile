####################################################################
# Makefile for building the students application
#


#
# Definitions
#

CC = g++ -Wall -std=c++11
CFLAGS = g++ -Wall -std=c++11
CCLINK = $(CC)
OBJS = tmp.o coordinate.o channel_gnss.o TimeUtils.o StringUtils.o FileIO.o pch.o Rinex3Obs.o Rinex3Nav.o Rinex2Obs.o Rinex2Nav.o RinexReader.o  gpssim.o 
RM = rm -f
TARGET = gps-sdr-sim

#
# Target Section
#
$(TARGET): $(OBJS)
	$(CCLINK) -o $(TARGET) $(OBJS)


#
# File Section
#
 
gpssim.o: .user-motion-size  gpssim.h misc.h
tmp.o: tmp.h
RinexReader.o: RinexReader.h

RinexReader.o: RinexReader.cpp pch.h Rinex2Nav.h Rinex2Obs.h Rinex3Nav.h Rinex3Obs.h FileIO.h StringUtils.h
 
Rinex2Nav.o: Rinex2Nav.cpp Rinex2Nav.h
Rinex2Obs.o: Rinex2Obs.cpp Rinex2Obs.h
Rinex3Nav.o: Rinex3Nav.cpp Rinex3Nav.h
Rinex3Obs.o: Rinex3Obs.cpp Rinex3Obs.h
pch.o: pch.cpp pch.h
FileIO.o: FileIO.cpp FileIO.h
StringUtils.o: StringUtils.cpp StringUtils.h
TimeUtils.o: TimeUtils.cpp TimeUtils.h
coordinate.o: coordinate.cpp coordinate.h
channel_gnss.o: channel_gnss.cpp channel_gnss.h

.user-motion-size: .FORCE
	@if [ -f .user-motion-size ]; then \
		if [ "`cat .user-motion-size`" != "$(USER_MOTION_SIZE)" ]; then \
			echo "Updating .user-motion-size"; \
			echo "$(USER_MOTION_SIZE)" >| .user-motion-size; \
		fi; \
	else \
		echo "$(USER_MOTION_SIZE)" > .user-motion-size; \
	fi;

#
# Cleaning
#
clean:
	$(RM) $(TARGET) $(OBJS) *.o *.bak *~"#"* core
	
.FORCE:

YEAR?=$(shell date +"%Y")
Y=$(patsubst 20%,%,$(YEAR))
%.$(Y)n:
	wget -q ftp://cddis.gsfc.nasa.gov/gnss/data/daily/$(YEAR)/brdc/$@.Z -O $@.Z
	uncompress $@.Z
