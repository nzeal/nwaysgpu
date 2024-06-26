.PHONY: all clean profile run

COMPILER = nvhpc

ifeq ($(COMPILER),gnu)
	CC = gcc
	OPTFLAGS = -O3 -g
	CFLAGS = -std=c99 -fopenmp $(OPTFLAGS) -lrt
	LDFLAGS = -fopenmp -lrt -lm
endif

ifeq ($(COMPILER),nvhpc)
	CC = nvc
	OPTFLAGS = -O3 -fast
	GPUFLAGS = -gpu=cc80,cuda12.3,pinned -Minfo=accel,inline
	CFLAGS = -acc $(OPTFLAGS) $(GPUFLAGS) --diag_suppress=implicit_func_decl
	LDFLAGS = -lm
endif

# Source and target files
SRC_FILES = laplace2d.c
TARGET = laplace2d # Final executable name

all: $(TARGET)

$(TARGET): $(SRC_FILES)
	$(CC) $(CFLAGS) $(LDFLAGS) -o $(TARGET) $(SRC_FILES)

NSYS = nsys profile
NSYSFLAGS = --stats=true --force-overwrite=true

REPORT_FOLDER = reports
profile: $(TARGET)
	mkdir -p $(REPORT_FOLDER)
	$(NSYS) $(NSYSFLAGS) -o $(REPORT_FOLDER)/report ./$(TARGET)

ncu: $(TARGET)
	 mkdir -p $(REPORT_FOLDER)
	 cd $(REPORT_FOLDER) && ncu -o profile ../$(TARGET)

clean:
	rm -rf $(TARGET) report *.qdrep *.sqlite reports

run: out/log.txt

out/log.txt: $(TARGET)
	mkdir -p out
	./$(TARGET) > $@
