# Copyright lowRISC contributors.
# Licensed under the Apache License, Version 2.0, see LICENSE for details.
# SPDX-License-Identifier: Apache-2.0

subdir('base')
subdir('arch')
subdir('runtime')
subdir('testing')
subdir('dif')

# UART library (sw_lib_uart)
sw_lib_uart = declare_dependency(
  link_with: static_library(
    'uart_ot',
    sources: ['uart.c'],
    dependencies: [
      sw_lib_base_print,
      sw_lib_runtime_ibex,
      dif_uart,
      top_earlgrey,
    ],
  )
)

# Flash controller library (sw_lib_flash_ctrl)
sw_lib_flash_ctrl = declare_dependency(
  link_with: static_library(
    'flash_ctrl_ot',
    sources: [
      hw_ip_flash_ctrl_reg_h,
      'flash_ctrl.c',
    ],
    dependencies: [
      top_earlgrey,
    ]
  )
)

# PINMUX library (sw_lib_pinmux)
sw_lib_pinmux = declare_dependency(
  link_with: static_library(
    'pinmux_ot',
    sources: [
      hw_top_earlgrey_pinmux_reg_h,
      'pinmux.c',
    ],
    dependencies: [
      top_earlgrey,
    ]
  )
)

# AES library (sw_lib_aes)
sw_lib_aes = declare_dependency(
  link_with: static_library(
    'aes_ot',
    sources: [
      hw_ip_aes_reg_h,
      'aes.c',
    ],
    dependencies: [
      top_earlgrey,
    ]
  )
)

# HMAC library (sw_lib_hmac)
sw_lib_hmac = declare_dependency(
  link_with: static_library(
    'hmac_ot',
    sources: [
      hw_ip_hmac_reg_h,
      'hw_sha256.c',
      'hmac.c',
    ],
    dependencies: [
      sw_lib_mem,
      top_earlgrey,
    ]
  )
)

# IRQ library (sw_lib_irq)
sw_lib_irq = declare_dependency(
  link_with: static_library(
    'irq_ot',
    sources: [
      'irq.c',
    ],
  )
)

# IRQ Handlers Library
#
# handler.c contains various definitions with weak linkage, for symbols
# referenced in irq_vectors.S
#
# To override default handlers, use the definitions in handler.h, and either
# link to this library to pick up the other default definitions, or include
# irq_vectors.S as a source dependency.
sw_lib_irq_handlers = declare_dependency(
  # The IRQ handler definitions need to be included as a "source" rather than
  # as part of a static library; this ensures that it is linked in as a .o
  # file, so the .vectors section is picked up.
  sources: ['irq_vectors.S'],
  link_with: static_library(
    'irq_default_handlers_ot',
    sources: [
      'handler.c',
    ],
    dependencies: [
      sw_lib_irq,
      sw_lib_runtime_ibex,
      sw_lib_uart,
    ],
  )
)

# RV_TIMER library (sw_lib_rv_timer)
sw_lib_rv_timer = declare_dependency(
  link_with: static_library(
    'rv_timer_ot',
    sources: [
      hw_ip_rv_timer_reg_h,
      'rv_timer.c',
    ],
    dependencies: [
      sw_lib_runtime_ibex,
      top_earlgrey,
    ],
  )
)

# SPI device library (sw_lib_spi_device)
sw_lib_spi_device = declare_dependency(
  link_with: static_library(
    'spid_ot',
    sources: [
      hw_ip_spi_device_reg_h,
      'spi_device.c',
    ],
    dependencies: [
      top_earlgrey,
    ]
  )
)

# USB DEV library (sw_lib_usb)
sw_lib_usb = declare_dependency(
  link_with: static_library(
    'usb_ot',
    sources: [
      hw_ip_usbdev_reg_h,
      'usb_controlep.c',
      'usb_simpleserial.c',
      'usbdev.c',
    ],
    dependencies: [
      sw_lib_uart,
      top_earlgrey,
    ]
  )
)
