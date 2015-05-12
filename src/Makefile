.PHONY:	all clean

PROGS = server client 
all:	$(PROGS)

clean:
	rm -rf *.o $(PROGS) grpc thrift *.tag

include Makefile.protocol.inc

CXXFLAGS += -std=c++11 -O3 -g $(EXTRA_CXXFLAGS)
LDFLAGS += $(EXTRA_LDFLAGS)
LDLIBS += $(PROTOCOL_LIBS) -lboost_timer -lboost_chrono -lboost_program_options -lboost_log -lboost_thread -lboost_system $(EXTRA_LIBS) -lpthread -lrt -ldl

X_HEADERS = $(patsubst %.h, plugin/%.h, $(EXTRA_HEADERS))
X_OBJS = $(patsubst %.cpp, plugin/%.o, $(EXTRA_SOURCES))

HEADERS = donkey.h $(X_HEADERS)

TAGS = protocol.tag
SERVER_OBJS = server.o $(PROTOCOL_OBJS)
CLIENT_OBJS = client.o $(PROTOCOL_OBJS)

server:	$(TAGS) $(SERVER_OBJS) $(HEADERS)  
	$(CXX) $(LDFLAGS) $(SERVER_OBJS) $(LDLIBS) -o $@ 

client:	$(TAGS) $(CLIENT_OBJS) $(HEADERS)
	$(CXX) $(LDFLAGS) $(SERVER_OBJS) $(LDLIBS) -o $@ 

build-info:	build-info.cpp $(HEADERS)
	$(CXX) $(LDFLAGS) build-info.cpp $(LDLIBS) -o $@
