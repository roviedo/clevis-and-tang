FROM fedora:latest

# RUN dnf check-update -y && dnf install firefox -y && dnf install vim -y && dnf install tang -y

RUN dnf update -y && dnf install vim -y && dnf install firefox -y && dnf install tang -y && dnf install systemd -y

# RUN systemctl enable tangd.socket --now

# ENTRYPOINT ["/lib/systemd/systemd"]