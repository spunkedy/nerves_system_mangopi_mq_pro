# MangoPi MQ Pro Support

[![CircleCI](https://circleci.com/gh/fhunleth/nerves_system_mangopi_mq_pro.svg?style=svg)](https://circleci.com/gh/fhunleth/nerves_system_mangopi_mq_pro)
[![Hex version](https://img.shields.io/hexpm/v/nerves_system_mangopi_mq_pro.svg "Hex version")](https://hex.pm/packages/nerves_system_mangopi_mq_pro)

This is the base Nerves System configuration for the [MangoPi MQ Pro](#mangopi).

*This is a work in progress. It may change in backwards incompatible ways and the documentation might be lacking.*

To do:

- [x] Bring up WiFi
- [ ] Verify Blue PWM LED (was working with Linux 5.14, but broke with 5.18)
- [?] Fix MicroSD flakiness on boot
- [x] Verify USB host-only port (works with USB Flash drive)
- [ ] Fix USB gadget mode on OTG port
- [ ] Verify SPI
- [ ] Verify I2C
- [ ] Verify all GPIO work
- [x] Verify HW watchdog
- [x] Check that `TARGET_GCC_FLAGS` are right
- [x] Update Linux kernel to 5.18
- [x] Implement A/B firmware updates work
- [x] Use SID for serial number
- [ ] Reduce prints and shorten boot time
- [ ] Verify HDMI

![MangoPi MQ Pro](assets/images/mq-pro-pink-t.png)
<br><sup>[Image credit](#mangopi)</sup>

| Feature              | Description                     |
| -------------------- | ------------------------------- |
| CPU                  | 1 GHz 64 bit RISC-V             |
| Memory               | 512 MB or 1 GB DRAM             |
| Storage              | MicroSD                         |
| Linux kernel         | 5.18 w/ patches                 |
| IEx terminal         | UART `ttyS0`                    |
| GPIO, I2C, SPI       | Yes - [Elixir Circuits](https://github.com/elixir-circuits) |
| Display              | Yes, but not supported yet      |
| ADC                  | Yes                             |
| PWM                  | Yes, but no Elixir support      |
| UART                 | ttyS0                           |
| Camera               | None                            |
| Ethernet             | No                              |
| WiFi                 | Onboard WiFi                    |
| RTC                  | No                              |
| HW Watchdog          | Yes                             |

## Using

The most common way of using this Nerves System is create a project with `mix
nerves.new` and add `mangopi` references where needed and in a similar way
to the default systems like `bbb`, etc. Then export `MIX_TARGET=mangopi`.
See the [Getting started
guide](https://hexdocs.pm/nerves/getting-started.html#creating-a-new-nerves-app)
for more information.

If you need custom modifications to this system for your device, clone this
repository and update as described in [Making custom
systems](https://hexdocs.pm/nerves/customizing-systems.html).

## Example use

This example assumes some familiarity with Nerves. To use this system, you'll
need OTP 25. Follow the [Nerves installation
instructions](https://github.com/nerves-project/nerves/blob/main/docs/Installation.md)
for additional system dependencies.

Creating a new hello world application:

```sh
mix nerves.new hello_mango
cd hello_mango
```

Open up your `mix.exs` and add `:mangopi_mq_pro` to the `@all_targets` list at
the top. It's ok to delete targets that you don't plan on using.

Then add the `:nerves_system_mango_mq_pro` dependency to the `deps` function:

```elixir
    {:nerves_system_mangopi_mq_pro, "~> 0.1", runtime: false, targets: :mangopi_mq_pro},
```

This will load the latest released version. To use the latest code on the `main`
branch here, add the following line:

```elixir
    {:nerves_system_mangopi_mq_pro, runtime: false, targets: :mangopi_mq_pro, nerves: [compile: true], git: "https://github.com/fhunleth/nerves_system_mangopi_mq_pro", branch: "main"}
```

To build and write to a MicroSD card, run:

```sh
export MIX_TARGET=mangopi_mq_pro
mix deps.get
mix firmware
mix burn
```

## Console access

The console is configured to output to the UART on pins 8 and 10 on the 40-pin
GPIO connector. This is just like the Raspberry Pi. A 3.3V FTDI cable is needed
to access the output.

## Networking

The board has two network interfaces, a WiFi module and a virtual Ethernet on
the USB C connector marked "OTG".

## Thanks

The most helpful Allwinner D1 information comes from
[linux-sunxi.org/Allwinner_Nezha](https://linux-sunxi.org/Allwinner_Nezha). All
of the work here wouldn't have been possible with out it. Thanks especially to
[smaeul's Allwinner D1 Linux fork](https://github.com/smaeul/linux/tree/riscv/d1-wip/arch/riscv)

[Image credit](#mangopi): This image is from [mangopi.cc](https://mangopi.cc/mangopi_mqpro).

