# NSteamLink v0.7.3

## 简体中文

## [0.7.3] - 2026-10-24

上一正式版：**v0.7.2**。目标分支：`main`；源码：[`v0.7.3`](https://github.com/kxn/nsteamlink/tree/v0.7.3)。

### 主要变化

- Switch 客户端向 Steam 上报的手柄身份改为 Nintendo Switch Pro Controller：HID VID/PID 为 `057e:2009`，产品名为 `Nintendo Switch Pro Controller`，feature caps 的 controller type 为 38。Steam 因此可按 NS Pro 识别手柄，而不再显示为 `0000:0000` 的通用手柄。
- 报告格式保持不变：仍使用 Generic RAW V3 与 `is_generic_gamepad=true`，不切换到 Switch 原生 HID 报告，也不改变按键、摇杆、陀螺仪的线上布局。
- 流式请求中预留的手柄槽位仍不填 `controller_type`，由 host 根据 HID vid:pid 判型。

### 验证与范围

在 `10.10.10.66` 真机部署验证：日志显示 `HID: Device found: sdl://0, id=057e:2009, name=Nintendo Switch Pro Controller`，随后 `StartInputReports(id=1, length=73)`，串流启动且 HID 报告持续提交；用户确认测试可用。本次只验证身份与串流启动，不声称 Steam 侧 ABXY、震动、陀螺仪已逐项回归，也不声称实现了真实 Pro Controller HID 协议。

### 提交分组

- 手柄身份：`d8ee4a7`（ihslib）Switch 上报 `057e:2009`、产品名与 feature caps 38。
- 发布：更新版本号、中英双语说明与 Release Notes。

[完整变更：v0.7.2 → v0.7.3](https://github.com/kxn/nsteamlink/compare/v0.7.2...v0.7.3)

---

## English

## [0.7.3] - 2026-10-24

Previous stable release: **v0.7.2**. Target: `main`; source: [`v0.7.3`](https://github.com/kxn/nsteamlink/tree/v0.7.3).

### Highlights

- Report the Nintendo Switch Pro Controller identity to Steam: HID VID/PID `057e:2009`, product string `Nintendo Switch Pro Controller`, and feature caps controller type 38. Steam can now type the pad as a Switch Pro instead of an unnamed `0000:0000` generic controller.
- Keep the report format unchanged: Generic RAW V3 with `is_generic_gamepad=true`; do not switch to a native Switch HID report or change the button, stick or gyro wire layout.
- Leave `ReservedGamepad.controller_type` unset so the host types the slot from HID vid:pid.

### Validation and scope

Verified on the Switch at `10.10.10.66`: `HID: Device found: sdl://0, id=057e:2009, name=Nintendo Switch Pro Controller`, followed by `StartInputReports(id=1, length=73)`. Streaming started and HID reports continued; the user judged the build usable. This verifies identity and stream start only. It does not claim item-by-item host-side ABXY, rumble or gyro regression, nor a native Pro Controller HID implementation.

### Commits by type

- Controller identity: `d8ee4a7` (ihslib) report `057e:2009`, product name and feature caps 38 on Switch.
- Release: version, bilingual notes and Release Notes.

[Full changelog: v0.7.2 → v0.7.3](https://github.com/kxn/nsteamlink/compare/v0.7.2...v0.7.3)
