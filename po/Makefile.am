POTFILESIN = $(shell grep -v '^\#' $(srcdir)/POTFILES.in)
POTFILES = $(POTFILESIN:%=$(top_srcdir)/%)
LINGUAS = $(shell cat $(srcdir)/LINGUAS)
MOFILES = $(LINGUAS:=.mo)
POFILES = $(LINGUAS:=.po)

noinst_DATA = $(MOFILES)

SUFFIXES = .mo

.po.mo:
	rm -f  && $(MSGFMT) -o $@ $<

clean-local:
	rm -f $(MOFILES)

install-data-hook: all
	linguas="$(LINGUAS)"; \
	for l in $$linguas; do \
	  dir="$(DESTDIR)$(datadir)/locale/$$l/LC_MESSAGES"; \
	  $(mkdir_p) $$dir; \
	  echo Installing $$l.mo to $$dir/$(PACKAGE).mo ; \
	  $(INSTALL_DATA) $$l.mo $$dir/$(PACKAGE).mo; \
	done

$(GETTEXT_PACKAGE).pot: $(POTFILES) Makefile
	rm -f $@ && \
	xgettext --directory=$(top_srcdir) \
	  --add-comments --keyword=_ --keyword=N_ \
	  --files-from=$(srcdir)/POTFILES.in --from-code=UTF-8 \
	  --package-name="@PACKAGE@" --package-version="@VERSION@" \
	  --msgid-bugs-address=openconnect-devel@lists.infradead.org -o $@

EXTRA_DIST = $(POFILES) LINGUAS POTFILES.in