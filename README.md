# A high-performance diagnostic tool for real-time CPU, RAM, and Network health.
import psutil
import time
from datetime import datetime

class SystemSentinel:
    @staticmethod
    def get_metrics():
        return {
            "time": datetime.now().strftime("%H:%M:%S"),
            "cpu_usage": f"{psutil.cpu_percent()}%",
            "ram_used": f"{psutil.virtual_memory().percent}%",
            "net_sent": f"{psutil.net_io_counters().bytes_sent / (1024**2):.2f} MB"
        }

if __name__ == "__main__":
    print("🚀 Monitoring Started (Press Ctrl+C to stop)")
    try:
        while True:
            metrics = SystemSentinel.get_metrics()
            print(f"[{metrics['time']}] CPU: {metrics['cpu_usage']} | RAM: {metrics['ram_used']} | Data Sent: {metrics['net_sent']}", end="\r")
            time.sleep(1)
    except KeyboardInterrupt:
        print("\n🛑 Sentinel Terminated.")
