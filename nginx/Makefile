
SDK_DIR = sdk/nginx-1.10.0

MODULE_SRCS = nginx/ngx_http_js_module_modules.c nginx/ngx_http_js_module.c nginx/ngx_http_js_parser.c

MODULE_OBJS  = $(subst nginx/, build/, $(subst .c,.o,$(MODULE_SRCS) ))

dynmodule: $(NXT_BUILDDIR)/libnxt.a $(NXT_BUILDDIR)/libnjs.a $(MODULE_OBJS)
	$(NXT_CC) -o $(NXT_BUILDDIR)/ngx_http_js_module.so $(MODULE_OBJS) $(NXT_BUILDDIR)/libnjs.a  -lm -shared -Wl,-undefined,dynamic_lookup
	@echo "Dynamic module compiled: " $(NXT_BUILDDIR)/ngx_http_js_module.so 


$(NXT_BUILDDIR)/%.o: nginx/%.c
	@echo "Compiling $<"
	@$(NXT_CC) -c -fPIC -pipe  -O -Wall -Wextra -Wpointer-arith -Wno-unused-parameter \
		-Wno-deprecated-declarations -Werror -g \
		-I $(SDK_DIR)/src/core \
		-I $(SDK_DIR)/src/event \
		-I $(SDK_DIR)/src/event/modules \
		-I $(SDK_DIR)/src/os/unix \
		-I $(SDK_DIR)/objs \
		-I $(SDK_DIR)/src/http \
		-I $(SDK_DIR)/src/http/v2 \
		-I $(SDK_DIR)/src/http/modules \
		-I nxt -I njs \
		-D NGX_STANDALONE_MODULE_BUILD \
		$(NGX_INCL_OPT) \
		-o $@ $<

$(NXT_BUILDDIR)/ngx_http_js_module_modules.o: $(SDK_DIR)/objs/ngx_http_js_module_modules.c
	@echo "Compiling $<"
	@$(NXT_CC) -c -fPIC -pipe  -O -Wall -Wextra -Wpointer-arith -Wno-unused-parameter \
		-Wno-deprecated-declarations -Werror -g \
		-I $(SDK_DIR)/src/core \
		-I $(SDK_DIR)/src/event \
		-I $(SDK_DIR)/src/event/modules \
		-I $(SDK_DIR)/src/os/unix \
		-I $(SDK_DIR)/objs \
		-I $(SDK_DIR)/src/http \
		-I $(SDK_DIR)/src/http/modules \
		-I nxt -I njs \
		$(NGX_INCL_OPT) \
		-o $@ $<


