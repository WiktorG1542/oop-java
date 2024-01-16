szukanie procesów z czymś ważnym:

```bash
ps aux | awk '$7 == "pts/1"'
```

`ojciec.sh`:

```bash
#!/bin/bash

# clear
echo -n "Podaj liczbe naturalna: "
read x
./syn.sh "$x" &  # Run syn.sh in the background with the user input
ojc_wynik=$((x*x))
wait $!  # Wait for the completion of the last background process (./syn.sh)
syn_wynik=$?
echo "Wynik obliczenia: $((ojc_wynik + syn_wynik))"
exit 0
```

`syn.sh`:

```bash
#!/bin/bash

y=$1
exit $((2 * y))
```

wynik odpalenia `./ojciec.sh`:

```text
Podaj liczbe naturalna: 4
Wynik obliczenia: 24
```

--------------------------------------------------------------------------------

do takiego skryptu:

```bash
#!/bin/bash

# Variable to track whether SIGINT should be handled
handle_sigint=true

# Function to handle SIGINT
handle_sigint() {
    if $handle_sigint; then
        echo "Jestem nieśmiertelny."
    fi
}

# Function to handle SIGHUP
handle_sighup() {
    handle_sigint=false
    echo "Przestaję reagować na SIGINT."
}

# Set up signal handlers
trap handle_sigint SIGINT
trap handle_sighup SIGHUP

# Infinite loop
while true; do
    sleep 1
done
```

wysyłamy w ten sposób:

```bash
pkill -SIGINT -f zadanie3.sh
pkill -SIGHUP -f zadanie3.sh
```

--------------------------------------------------------------------------------

`script1.sh`:

```bash
#!/bin/bash

trap ./napis.sh USR1
trap ./koniec.sh USR2

while true
do
    sleep 5
done

exit 0
```

`napis.sh`:

```bash
#!/bin/bash

echo "Napis skryptu napis.sh"
```

`koniec.sh`:

```bash
#!/bin/bash

echo "Przerwanie skryptu!"
kill -9 $PPID
exit 0
```

odpalasz `./script1.sh`, potem wysyłasz sygnały:

```bash
pkill -USRX -f script1.sh
```