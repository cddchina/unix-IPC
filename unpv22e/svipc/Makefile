include ../Make.defines

PROGS =	ftok ftok1

all:	${PROGS}

ftok:	ftok.o
		${CC} ${CFLAGS} -o $@ ftok.o ${LIBS}

ftok1:	ftok1.o
		${CC} ${CFLAGS} -o $@ ftok1.o ${LIBS}


clean:
		rm -f ${PROGS} ${CLEANFILES}
