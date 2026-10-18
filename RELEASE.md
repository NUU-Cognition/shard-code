# 0.1.5

- One workflow for each mode (NUU Orbh Task 748). `wkfl-code-do_mission` has `> [!headless]` callouts in its stages, and `init-code` has a `# Headless` section. `hwkfl-code-do_mission` and `hinit-code` are deleted. A headless session loads the shard with `flint shard start code`.

# 0.1.4

- The dependency on the Flint shard accepts any version (`"@nuucognition/flint": ""`), so the shard works with Flint 0.3.x and with Flint 0.4.0 (NUU Flint Task 1129).

# 0.1.0

- Initial shard scaffold
