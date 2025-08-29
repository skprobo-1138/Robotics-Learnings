# Lecture 1 — Building a ROS 2 Workspace (Underlay & Overlay)

> Goal: Create a ROS 2 *overlay* workspace on top of your main ROS 2 *underlay*, fetch example packages, resolve dependencies, and build with `colcon`.

---

## What are Underlays & Overlays?

**Underlay**  
- Your *base* ROS 2 installation (e.g., `/opt/ros/humble` on Linux/macOS, or `C:\dev\ros2_humble` on Windows).  
- Provides “already-built” packages and tools that your projects can use.  
- You “activate” it by **sourcing** its `setup` script.

**Overlay**  
- Your *development* workspace that sits **on top of** the underlay.  
- When you build your overlay, it generates its own `install` folder with another `setup` script.  
- After sourcing the overlay, the shell will prefer packages from the overlay (your edited code) over the underlay.  
- This lets you test changes **without** touching the base installation.

**How it works (conceptually):**
1. Source underlay → your environment knows about core ROS 2 packages.
2. Build overlay → creates `install/` with your packages.
3. Source overlay → environment paths now point to your overlay **first**, then fall back to underlay.

**Example:**  
- Underlay has `turtlesim` v1.  
- You clone/modify `turtlesim` in your overlay and build.  
- After sourcing the overlay, running `ros2 run turtlesim turtlesim_node` uses your **overlay** version.  
- Open a **fresh terminal** (no overlay sourced) to fall back to the underlay version.

---

## Prerequisites

- ROS 2 Humble (or your target distro) installed.
- Developer tools:
  - **Linux/macOS:** `git`, `python3-rosdep`, `colcon`, build tools (`build-essential`, etc.).
  - **Windows:** Visual Studio (Desktop C++), Python3, `colcon`. Use the **x64 Native Tools Command Prompt**.

> Replace `humble` below if you’re using another ROS 2 distro.

---

## Task 1 — Source ROS 2 Environment (Underlay)

This makes the base install (underlay) available to the shell.

**Linux (bash)**
```bash
source /opt/ros/humble/setup.bash
