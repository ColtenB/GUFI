GTEST_BUILD_DIR   ?= ../../googletest/build
GTEST_INSTALL_DIR ?= ../../googletest/install

CC?=gcc
CXX?=g++
CFLAGS=-Wall -g3 -O0 -I$(GTEST_INSTALL_DIR)/include/
LDFLAGS=-L$(GTEST_INSTALL_DIR)/lib64 -lgtest -lgtest_main -lpthread

TARGET=test
TESTS=empty
OBJ=$(addsuffix .o, $(TESTS))

all: $(GTEST_INSTALL_DIR) $(TARGET)

$(GTEST_INSTALL_DIR):
	mkdir -p $(GTEST_BUILD_DIR) && cd $(GTEST_BUILD_DIR) && cmake -DCMAKE_INSTALL_PREFIX=$(GTEST_INSTALL_DIR) ..
	$(MAKE) -C $(GTEST_BUILD_DIR) install

$(TARGET): $(OBJ)
	$(CXX) $(CFLAGS) $^ $(LDFLAGS) -o $@

%.o: %.c $(GTEST_INSTALL_DIR)
	$(CC) $(CFLAGS) -c $< -o $@

%.o: %.cc $(GTEST_INSTALL_DIR)
	$(CXX) $(CFLAGS) -c $< -o $@

%.o: %.cpp $(GTEST_INSTALL_DIR)
	$(CXX) $(CFLAGS) -c $< -o $@

run: $(TARGET)
	./$<

clean:
	rm -rf $(OBJ) $(TARGET)