# $Id$

FILES=		portshaker.conf
FILESDIR_portshaker.conf=	${ETCDIR}

SUBDIR=		portshaker.d

main_merge_from=	ports
.if defined (WITH_BSDSHARP)
main_merge_from+=	github:smortex:bsd-sharp
.endif
.if defined (WITH_ENLIGHTENMENT)
main_merge_from+=	enlightenment
.endif
.if defined (WITH_GECKO)
main_merge_from+=	gecko
.endif
.if defined (WITH_HASKELL)
main_merge_from+=	haskell
.endif
.if defined (WITH_MARCUSCOM)
main_merge_from+=	marcuscom_ports
.endif
.if defined (WITH_TEXLIVE)
main_merge_from+=	github:smortex:freebsd-texlive github:smortex:freebsd-texlive:releng
.endif
.if defined (WITH_XORG)
main_merge_from+=	xorg
.endif

portshaker.conf: portshaker.conf.part
	@echo "  GEN    portshaker.conf"
	@cp portshaker.conf.part portshaker.conf
	@echo "main_merge_from=\"${main_merge_from}\"" >> portshaker.conf

clean:
	rm -f portshaker.conf

.include <bsd.prog.mk>

all beforeinstall:
.if ! exists(${ETCDIR}/portshaker.d)
	@echo " ,----------------------------( Error )----------------------------."
	@printf " | The %-59s |\n" "'${ETCDIR}/portshaker.d' directory does not exist."
	@echo " |                                                                 |"
	@echo " | Ensure that portshaker(8) is installed and \$$PREFIX is set       |"
	@echo " | properly, then try again.                                       |"
	@echo " \`-----------------------------------------------------------------'"
	@false
.endif
.if ! defined (WITH_BSDSHARP) && \
    ! defined (WITH_ENLIGHTENMENT) && \
    ! defined (WITH_GECKO) && \
    ! defined (WITH_HASKELL) && \
    ! defined (WITH_MARCUSCOM) && \
    ! defined (WITH_TEXLIVE) && \
    ! defined (WITH_XORG)
	@echo " ,----------------------------( Error )----------------------------."
	@echo " | You have to define at least one of the following to generate a  |"
	@echo " | sample portshaker.conf that fits your needs:                    |"
	@echo " |   - WITH_BSDSHARP      -- Merge BSD# team's developement ports; |"
	@echo " |   - WITH_ENLIGHTENMENT -- Merge E17 work in progress ports;     |"
	@echo " |   - WITH_GECKO         -- Merge Gecko's ports;                  |"
	@echo " |   - WITH_HASKELL       -- Merge Haskell's ports;                |"
	@echo " |   - WITH_MARCUSCOM     -- Merge GNOME team's development ports; |"
	@echo " |   - WITH_TEXLIVE       -- Merge unofficial TeXLive ports.       |"
	@echo " |   - WITH_XORG          -- Merge Xorg development ports.         |"
	@echo " \`-----------------------------------------------------------------'"
	@false
.endif
