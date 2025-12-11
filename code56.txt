

# PROG-6 (Data viz ggplot2)



library(ggplot2)
library(dbplyr)
library(reshape2)

data("mpg")
head(mpg)

ggplot(mpg,aes(x = displ,y = hwy,color = class)) +
  geom_point(size=3,alpha = 0.7) +
  geom_smooth(method = "lm", se = TRUE, linetype = "dashed", linewidth = 1, color = "black") +
  labs(
    title = "Scatter Plot of Engine Displacement vs Highway MPG wit Regression Line",
    x = "Engine Displacement (L)",
    y = "Highway Miles per Gallon",
    color = "Vehicle Class"
  ) +
  theme_bw()

ggplot(mpg,aes(x = displ,y = hwy)) +
  geom_point(color = "green") +
  facet_wrap(facets = ~class, ncol = 2) +
  labs(
    title = "Faceted Scatter Plot by Vehicle Class",
    x = "Engine Displacement",
    y = "Highway miles per gallon"
  )

data("diamonds")
print(diamonds)

cor_matrix <- cor(diamonds[, sapply(diamonds, is.numeric)], use = "complete.obs")
print(cor_matrix)

cor_data <- melt(cor_matrix)
print(cor_data)

ggcorrplot(
  cor_matrix,
  title = "HeatMap of correlation matrix",
  ggtheme = theme_bw(),
  method = "circle"
)

ggplot(mpg, aes(x = displ, y = hwy, color = class)) +
  geom_point(size = 3) +
  theme_classic() +
  scale_color_brewer(palette = "Set2") +
  labs(
    title = "Customized Scatter Plot with Aesthetic Enhancements",
    x = "Engine Displacement (L)",
    y = "Highway Miles per Gallon",
    color = "Class"
  )

annotated_plot <- ggplot(mpg, aes(x = displ, y = hwy, color = "class")) +
  geom_point(size = 2) +
  annotate("text", x = 3, y = 40, label = "High Efficiency Zone", color = "black", size = 5) +
  annotate("rect", xmin = 2, xmax = 4, ymin = 30, ymax = 45, fill = "yellow", color = "orange", alpha = 0.31) +
  labs(
    title = "Annotated Scatter Plot with Highlighted Zone",
    x = "Engine Displacement (L)",
    y = "Highway Miles per Gallon"
  ) +
  theme_classic()

annotated_plot

ggsave("annotatedplt.png", annotated_plot)
