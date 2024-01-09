

Introduction:
Configuring wakatime with Lazy may some time not work well specifically with distributions line NVChad. This article provides a step-by-step guide to effortlessly set up Wakatime in Neovim, ensuring that it is loaded, accompanied by the convenience of Lazy loading and Mason.

### Preloading Wakatime with Lazy Loading
To start, add the following lines to your setup function in the NV-Chad configuration to preload Wakatime upon Neovim's opening:

```lua
{
  "wakatime/vim-wakatime",
  lazy=false,
  setup = function ()
    vim.cmd([[packadd wakatime/vim-wakatime]])
  end
},
```

This ensures that Wakatime is loaded when Neovim opens. It also clones the plugin if not installed on opening nvim.

### Verifying Wakatime Installation
After preloading, Wakatime will be installed, but for it to be registered on newer versions of Neovim, the Wakatime CLI needs manual setup. Check your Neovim version using `:version` and consider updating to the latest version if necessary. I am using version `0.9.5`.

```sh
NVIM v0.9.5
Build type: Release
LuaJIT 2.1.1692716794

   system vimrc file: "$VIM/sysinit.vim"
  fall-back for $VIM: "/__w/neovim/neovim/build/nvim.AppDir/usr/share/nvim"

Run :checkhealth for more info
```

### Setting Up Wakatime CLI
Follow these steps to set up the Wakatime CLI manually for optimal integration:

1. Clone the Wakatime CLI repository:

```sh
git clone git@github.com:wakatime/wakatime-cli.git ~/wakatime-cli
# or
git clone https://github.com/wakatime/wakatime-cli.git ~/wakatime-cli
```

2. Build the Wakatime CLI using Go or install the binary [here](http://github.com/shadmeoli/nvim_wakatime_setup).

```sh
cd ~/wakatime-cli
go build
mv wakatime-cli ~/.wakatime/wakatime-cli
```

Ensure the generated binary is moved to the `.wakatime` folder.

If the folder doesn't exist, run Neovim to install the plugin with Mason, then quit Neovim or create the `.wakatime` folder manually and re-run the build process.

```sh
mkdir ~/.wakatime
cd ~/wakatime-cli
go build
mv wakatime-cli ~/.wakatime/wakatime-cli
```

### Configuring API Key
Open Neovim and set up the API key using the following command:

```sh
:WakaTimeApiKey
```

If the prompt to add the API Key does not appear, run the command mentioned above.

Copy your [API key](https://wakatime.com/settings/account#apikey) from Wakatime's website and paste it in the command palette. Hit enter, exit Neovim, and reopen it. Now, running `:WakaTimeToday` will display the time spent on coding.

Congratulations! You've successfully set up Wakatime in Neovim with Lazy loading and Mason, ensuring a smooth integration for effective code time tracking.