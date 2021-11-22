# Enable Function Keys On The Keychron K2/K4 Mechanical Keyboard Under Linux


Below, you'll find the steps required to create a systemd command that will run at boot to disable the media keys and restore f1-f12 functionality.

## Step 1

Open a terminal window and enter the following command:

`sudo nano /etc/systemd/system/keychron.service`

## **Step** 2

Paste the following into the window:

```
[Unit]
Description=The command to make the Keychron K2-k4 work with Function keys

[Service]
Type=oneshot
ExecStart=/bin/bash -c "sudo echo 1 | sudo tee /sys/module/hid_apple/parameters/fnmode"
ExecStop=/bin/bash -c "sudo echo 0 | sudo tee /sys/module/hid_apple/parameters/fnmode"

[Install]
WantedBy=multi-user.target
```

Press `ctrl+o` and then `ctrl+x` to exit.

## Step 3

In the terminal, type the following:

`sudo systemctl enable keychron`

## Step 4

That's it! A reboot, and you'll see that the function keys have been re-enabled.

## Tips

If you want to simply drag/drop the file that you create manually in the steps provided, I have it under the scripts folder in this repo. Download it and drop it in `/etc/systemd/system/`, doing Step 3 at the end.

Your keyboard renponds now first for the F1-F12 Keys, using **Fn** you can access the multimedia keys as well.

If you are using a model without the "PrintScreen Key", you can use it by pressing **Fn+PgUp** for about 4 seconds, than this key will turn into your "PrintScreen Key", if you want to revert to "PageUp", just repeat the process by holding **Fn+PgUp** for about 4 seconds again.
