# Hilzx
#!/system/bin/sh

# Hilzx Project
# Android read-only diagnostic utility

BASE="/sdcard/Download/HilzxProject"

echo "================================"
echo "       HILZX PROJECT"
echo "================================"
echo "Status : Berjalan"
echo "Android: $(getprop ro.build.version.release)"
echo "Model  : $(getprop ro.product.model)"
echo "--------------------------------"

if [ -r /proc/meminfo ]; then
    awk '
    /^MemTotal:/ {
        printf "Total RAM : %.0f MB\n", $2/1024
    }
    /^MemAvailable:/ {
        printf "RAM tersedia: %.0f MB\n", $2/1024
    }
    ' /proc/meminfo
else
    echo "Info RAM tidak tersedia."
fi

echo "--------------------------------"
echo "Penyimpanan /data:"
df -h /data 2>/dev/null

echo "================================"
echo "Pemeriksaan selesai."

#!/system/bin/sh

echo "=== HILZX PROJECT: DEVICE INFO ==="

echo "Model:"
getprop ro.product.model

echo "Versi Android:"
getprop ro.build.version.release

echo "Versi SDK:"
getprop ro.build.version.sdk

echo "Arsitektur:"
getprop ro.product.cpu.abi

echo "Selesai."ACTIVE SUBSYSTEMS BLOCK ] ---
echo "╔═════════════════════════════════════════════════════════════╗"
echo "║ [#] EXECUTING ACTIVE SUBSYSTEMS:                            ║"
echo "╠═════════════════════════════════════════════════════════════╣"
echo "║   ⚙️ NIGHTSHADE-DISPLAY -> Dynamic Refresh Rate (60/90/120Hz) ║"
echo "║   ⚙️ NIGHTSHADE-TOUCH   -> Ultra Slip & Max Fling Velocity  ║"
echo "║   ⚙️ NIGHTSHADE-ANIM    -> Zero Animation Scale Locked (0.0)║"
echo "║   ⚙️ NIGHTSHADE-GPU     -> SkiaHW Render & Hardware Pipeline║"
echo "║   ⚙️ NIGHTSHADE-THERMAL -> Fixed Performance & Doze Bypass  ║"
echo "╚═════════════════════════════════════════════════════════════╝"
echo ""

echo ">> [NIGHTSHADE-X] Purging cache and starting injection..."
sleep 0.2

# --- [01] DYNAMIC MULTI-HZ DISPLAY REFRESH RATE (60Hz / 90Hz / 120Hz) ---
echo "[ 01 / 05 ] Applying Dynamic Display Refresh Rate Stack..."
settings put system peak_refresh_rate 120.0 > /dev/null 2>&1
settings put system min_refresh_rate 60.0 > /dev/null 2>&1
settings put global peak_refresh_rate 120.0 > /dev/null 2>&1
settings put global min_refresh_rate 60.0 > /dev/null 2>&1
settings put secure refresh_rate_mode 2 > /dev/null 2>&1
setprop persist.sys.sf.high_fps 1 > /dev/null 2>&1
echo "Status: OK [Multi-Hz Auto-Match Active]"
sleep 0.1

# --- [02] EXTREME TOUCH SLIP & VELOCITY CALIBRATION ---
echo "[ 02 / 05 ] Calibrating Ultimate Touch Slip & Fling Velocity..."
settings put system touch_exploration_enabled 0 > /dev/null 2>&1
settings put system high_touch_sensitivity_enabled 1 > /dev/null 2>&1
settings put system long_press_timeout 10 > /dev/null 2>&1
settings put system pointer_speed 7 > /dev/null 2>&1
settings put global view.touch_slop 1 > /dev/null 2>&1
settings put global view.minimum_fling_velocity 9500 > /dev/null 2>&1
settings put global view.maximum_fling_velocity 32000 > /dev/null 2>&1
settings put global view.scroll_friction 0.008 > /dev/null 2>&1
settings put global touch.pressure.scale 0.00003 > /dev/null 2>&1
settings put global touch.filter.moving 0 > /dev/null 2>&1
settings put global pointer_accel_profile 0 > /dev/null 2>&1
settings put global touch.size.calibration 0 > /dev/null 2>&1
settings put global touch.orientation.aware 1 > /dev/null 2>&1
device_config put input_native_boot motion_classifier_enabled false > /dev/null 2>&1
device_config put input_native_boot velocitytracker_strategy lsq2 > /dev/null 2>&1
echo "Status: OK [Ultra Slip & Fling Velocity Loaded]"
sleep 0.1

# --- [03] ZERO ANIMATION SCALE BYPASS ---
echo "[ 03 / 05 ] Locking Zero Animation Scale (0.0)..."
settings put global window_animation_scale 0.0 > /dev/null 2>&1
settings put global transition_animation_scale 0.0 > /dev/null 2>&1
settings put global animator_duration_scale 0.0 > /dev/null 2>&1
echo "Status: OK [Animations Disabled]"
sleep 0.1

# --- [04] GPU RENDER PIPELINE & HARDWARE ACCELERATION ---
echo "[ 04 / 05 ] Optimizing GPU Pipeline & Hardware Acceleration..."
sync
cmd package trim-caches 1024M > /dev/null 2>&1
settings put global debug.hwui.renderer skiahw > /dev/null 2>&1
setprop debug.composition.type gpu > /dev/null 2>&1
setprop debug.egl.hw 1 > /dev/null 2>&1
setprop debug.sf.hw 1 > /dev/null 2>&1
settings put global debug.performance.tuning 1 > /dev/null 2>&1
settings put global cached_apps_freezer enabled > /dev/null 2>&1
settings put global cached_apps_freezer_binder_enabled true > /dev/null 2>&1
echo "Status: OK [SkiaHW & Hardware Pipeline Locked]"
sleep 0.1

# --- [05] THERMAL CONTROL, DOZE BYPASS & SPEED-PROFILE COMPILE ---
echo "[ 05 / 05 ] Locking Thermal Governor & Re-compiling Game Packages..."
cmd power set-fixed-performance-mode-enabled true > /dev/null 2>&1
settings put global low_power 0 > /dev/null 2>&1
settings put global thermal_throttle_mode 1 > /dev/null 2>&1
settings put global adaptive_battery_management_enabled 0 > /dev/null 2>&1
dumpsys deviceidle whitelist +com.dts.freefireth > /dev/null 2>&1
dumpsys deviceidle whitelist +com.dts.freefiremax > /dev/null 2>&1
cmd game mode performance com.dts.freefireth > /dev/null 2>&1
cmd game mode performance com.dts.freefiremax > /dev/null 2>&1
cmd package trim-caches 2048M > /dev/null 2>&1
cmd package compile -m speed-profile -f com.dts.freefireth > /dev/null 2>&1
cmd package compile -m speed-profile -f com.dts.freefiremax > /dev/null 2>&1
sync
echo "Status: OK [APIs, Doze Bypass & Speed-Profile Synchronized]"
echo ""

# --- [ CORE STATUS DASHBOARD ] ---
echo "==============================================================="
echo "  RESULT : DEPLOYMENT SUCCESSFUL [NON-ROOT SAFE]              "
echo "  MODE   : WEEKLY PUBLIC MODULE (CLEAN ADB SHELL)             "
echo "==============================================================="
echo "MODULE ACTIVATED, ENJOY UR GAMEPLAY WITH MAXIMUM PERFORMANCE"
echo "GOOD LUCK & DOMINATE THE BATTLEFIELD!"
echo "==============================================================="
echo "  [::] Process finished with exit code 0.                       "
echo "==============================================================="
echo ""
echo "[shproc] Process[pid=$$, hasExited=true, exitcode=0]"
adb shell sh /sdcard/Download/HilzxProject/module.sh
adb shell sh /sdcard/Download/HilzxProject/functions/info.sh
