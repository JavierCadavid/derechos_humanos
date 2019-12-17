library(ggplot2)  
library(tidyverse)  
library(scales)  
library(pinochet)


##
places1 <- pinochet %>% count(place_1) %>%
mutate(prop=n/sum(n))
dato_noNA <- places1[!is.na(places1$place_1),]

ggplot(dato_noNA, aes(place_1,n)) +
geom_bar(stat= "identity")

##
percent_bar2 <- dato_noNA %>% ##
arrange(desc(prop)) %>%
mutate(place_1 = factor(place_1, level= place_1))%>%
ggplot(aes(place_1, prop)) +
geom_bar(stat = "identity",
        fill = "light green",
        color = "black")
          

percent_bar2 +
geom_text(aes(label= percent((prop))),
          vjust = -0.3) +
labs(x = "Place_1",
    y = "%",
    title = "Places with the highest percentage of victims",
    subtitle = "Pinochet Regime, 1973-1990") +
scale_y_continuous(labels =percent) +
theme_classic()

ggsave('pinochet2.jpeg', width = 8, height = 4, units = 'in')

