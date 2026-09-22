
# ==============================================================================
#    sync3d  |  Quantum Geometric Alignment Engine
#    Hardware-Accelerated Multi-Trace 3D Animations via WebGL Injections
# ==============================================================================
#  Project:      sync3d (Synchronized 3D Vector Framework)
#  Author:       Katharina Maria Brecht
#  ORCID:        0009-0001-2176-7476
#  Philosophy:   Connecting discrete geometry with continuous time-waves.
# ------------------------------------------------------------------------------
#  This core function bypasses structural plotly rendering limits by
#  decoupling the computing pipeline into dual-layer processing.
# ==============================================================================
#' 3D Visualization Utility for Synchronizing Edges with Animated Markers
#'
#' @param base_plot An animated plotly 3D scatter plot (Trace 0).
#' @param edge_indices A matrix or data frame with 'from' and 'to' columns.
#' @return An expanded plotly widget with synchronized WebGL lines.
#' @examples
#' # Server-safe infrastructure test without generating interactive 'UI' windows
#' library(plotly)
#' mock_plot <- plot_ly()
#' mock_edges <- matrix(c(1, 2), ncol = 2)
#' tested_utility <- add_synchronized_3d_edges(mock_plot, mock_edges)
#' @import plotly
#' @export
add_synchronized_3d_edges <- function(base_plot, edge_indices) {

  # Uebergabe der Verbindungs-Indizes als Metadaten an das Widget
  # Pass custom edge indices as metadata to the widget
  base_plot$x$customEdgeIndices <- as.numeric(t(edge_indices))

  # Injektion der JavaScript-Erweiterung ueber htmlwidgets
  # Inject the JavaScript extension via htmlwidgets
  htmlwidgets::onRender(base_plot, "
    function(el, x) {
      var graphDiv = el;
      var indices = x.customEdgeIndices;
      if (!indices) return;

      function renderSyncLines() {
        var pts = graphDiv.data; // Zugriff auf Trace 0 (Knotenpunkte)
        if (!pts || !pts.x) return;

        var lx = [], ly = [], lz = [];

        for (var i = 0; i < indices.length; i += 2) {
          var idx1 = indices[i] - 1; // R (1-basiert) zu JS (0-basiert)
          var idx2 = indices[i+1] - 1;

          if (pts.x[idx1] !== undefined && pts.x[idx2] !== undefined) {
            lx.push(pts.x[idx1], pts.x[idx2], null);
            ly.push(pts.y[idx1], pts.y[idx2], null);
            lz.push(pts.z[idx1], pts.z[idx2], null);
          }
        }

        if (graphDiv.data.length < 2) {
          var lineTrace = {
            type: 'scatter3d',
            mode: 'lines',
            x: lx, y: ly, z: lz,
            line: {width: 2, color: '#666666'},
            opacity: 0.5,
            showlegend: false
          };
          Plotly.addTraces(graphDiv, lineTrace);
        } else {
          Plotly.restyle(graphDiv, {x: [lx], y: [ly], z: [lz]});
        }
      }

      el.then(function() {
        renderSyncLines();
        graphDiv.on('plotly_animated', function() {
          renderSyncLines();
        });
      });
    }
  ")
}

