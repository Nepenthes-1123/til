# WSL2上のDockerコンテナでのGUI

WSL2上のDockerコンテナで表示しているGUIをWindowsに表示する

## Dockerコンテナ

### 環境変数

- DISPLAY=$DISPLAY
- PULSE_SERVER=$PULSE_SERVER
- WAYLAND_DISPLAY=$WAYLAND_DISPLAY
- XDG_RUNTIME_DIR=$DXG_RUNTIME_DIR

### aptパッケージ

```bash
apt install -y python3-tk
```
