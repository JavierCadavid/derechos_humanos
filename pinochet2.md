library(ggplot2)  
library(tidyverse)  
library(scales)  
library(pinochet)


#

killed <- pinochet %>% count(violence) %>%
mutate(prop=n/sum(n))
dato2_noNA <- killed[!is.na(killed$violence),]


ggplot(dato2_noNA, aes(violence,n)) +
geom_bar(stat= "identity")

#
percent_bar <- dato2_noNA %>% ##
arrange(desc(prop)) %>%
mutate(violence = factor(violence, level= violence))%>%
ggplot(aes(violence, prop)) +
geom_bar(stat = "identity",
        fill = "Dark green",
        color = "black")
          

percent_bar +
geom_text(aes(label= percent((prop))),
          vjust = -0.3) +
labs(x = "Violence",
    y = "%",
    title = "Percentage of victims",
    subtitle = "Pinochet Regime, 1973-1990") +
scale_y_continuous(labels =percent) +
theme_classic()

ggsave('pinochet.jpeg', width = 8, height = 4, units = 'in')
  




