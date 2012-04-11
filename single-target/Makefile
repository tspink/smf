OUT	:= 
OBJ	:= 
PKG	:= 

LDFLAGS	:=
CFLAGS	:= -g -Wall

LDFLAGS	+= $(foreach P,$(PKG),`pkg-config --libs $(P)`)
CFLAGS	+= $(foreach P,$(PKG),`pkg-config --cflags $(P)`)

all:	$(OUT)

clean:
	$(RM) -f $(OBJ)
	$(RM) -f $(OUT)

$(OUT):	$(OBJ)
	$(CC) -o $@ $(LDFLAGS) $(OBJ)

%.o: %.c
	$(CC) -c -o $@ $(CFLAGS) $<
