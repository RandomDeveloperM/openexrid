sinclude ../makefile.myconfig
sinclude ../makefile.config

PWD = $(shell pwd)
SRCS := $(shell ls ../nuke/*.cpp)
OBJS = $(addprefix $(VERSION)/,$(addsuffix .o,$(basename $(notdir $(SRCS)))))

all: $(VERSION) $(VERSION)/DeepOpenEXRId.so

$(VERSION):	
	mkdir -p $(VERSION)

$(VERSION)/DeepOpenEXRId.so: $(OBJS)
	$(CXX) -o $@ $(OBJS) --shared $(LDFLAGS)

$(OBJS): $(VERSION)/%.o: $(PWD)/../nuke/%.cpp
	$(CXX) -c -I.. $(CPPFLAGS) -I $(NUKE_INCLUDE) $< -o $@

clean:
	rm -f $(VERSION)/*.o $(VERSION)/*.a $(VERSION)/*.d $(VERSION)/*.ofx

install: $(VERSION)/DeepOpenEXRId.so
	mkdir -p $(PREFIX)/$(NUKE_VERSION)
	cp $(VERSION)/DeepOpenEXRId.so $(PREFIX)/$(NUKE_VERSION)/
	strip $(PREFIX)/$(NUKE_VERSION)/DeepOpenEXRId.so
	cp $(VERSION)/DeepOpenEXRId.so ~/.nuke/
	cp ../nuke/menu.py ~/.nuke/

DEPS = $(SRCS:%.cpp=$(VERSION)/%.d)
sinclude $(DEPS)
