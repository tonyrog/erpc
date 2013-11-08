MODULES := pmap_xdr pmap_clnt rpc_xdr pmap rpc_client rpc_server
ERLC = erlc
EBIN = ../ebin
OBJECTS := $(MODULES:%=$(EBIN)/%.beam)
ERLC_FLAGS = -Wall

all: $(OBJECTS)

clean:
	rm -f $(OBJECTS) pmap_xdr.erl pmap.hrl pmap_clnt.erl rpc.hrl rpc_xdr.erl

pmap_xdr.erl: pmap.x
	erpcgen -a '[xdr]' pmap

pmap.hrl: pmap.x
	erpcgen -a '[hrl]' pmap

pmap_clnt.erl: pmap.hrl pmap.x
	erpcgen -a '[clnt]' pmap

rpc.hrl: rpc.x
	erpcgen -a '[hrl]' rpc

rpc_xdr.erl: rpc.x
	erpcgen -a '[xdr]' rpc

$(EBIN)/rpc_server.beam: rpc.hrl
$(EBIN)/rpc_client.beam: rpc.hrl
$(EBIN)/pmap.beam: pmap.hrl

$(EBIN)/%.beam: %.erl
	$(ERLC) $(ERLC_FLAGS) -o $(EBIN) $<
