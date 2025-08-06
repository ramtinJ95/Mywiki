# Eza setup
in .zshrc:
EZA_CONFIG_DIR=/Users/<username>/.config/eza
XDG_CONFIG_HOME=/Users/<username>/.config

clone the eza-theme repo into .config/eza and move out test and theme folder out
1 level so they are all on the same level inside the .config/eza folder.

Create symlink from applications to the eza folder:
mkdir ~/Library/Application\ Support/eza

cd ~/Library/Application\ Support/eza

ln -sf $EZA_CONFIG_DIR/eza-themes/themes/tokyonight.yml ./theme.yml

Test that everything worked properly:
eza -lh --icons $EZA_CONFIG_DIR/test_dir
