MODULES := pmap_xdr pmap_clnt rpc_xdr pmap rpc_client rpc_server
ERLC = erlc
EBIN = ../ebin
OBJECTS := $(MODULES:%=$(EBIN)/%.beam)
ERLC_FLAGS = -Wall

all: $(OBJECTS)

clean:
	rm -f $(OBJECTS) pmap_xdr.erl pmap.hrl pmap_clnt.erl rpc.hrl rpc_xdr.erl

pmap_xdr.erl: pmap.x
	erpcgen -xdr pmap.x

pmap.hrl: pmap.x
	erpcgen -hrl pmap.x

pmap_clnt.erl: pmap.hrl pmap.x
	erpcgen -clnt pmap.x

rpc.hrl: rpc.x
	erpcgen -hrl rpc.x

rpc_xdr.erl: rpc.x
	erpcgen -xdr rpc.x

$(EBIN)/rpc_server.beam: rpc.hrl
$(EBIN)/rpc_client.beam: rpc.hrl
$(EBIN)/pmap.beam: pmap.hrl

$(EBIN)/%.beam: %.erl
	$(ERLC) $(ERLC_FLAGS) -o $(EBIN) $<
