package me.Browk.qCratesExpansion;

import me.Browk.qCrates.Main;
import me.clip.placeholderapi.PlaceholderAPI;
import me.clip.placeholderapi.expansion.*;
import org.bukkit.*;
import org.bukkit.entity.*;

public class qCratesExpansion extends PlaceholderExpansion implements Cacheable {
    private me.Browk.qCrates.Main plugin;
    
    public boolean canRegister() {
        return Bukkit.getPluginManager().getPlugin(this.getPlugin()) != null;
    }
    
    public boolean register() {
    	if (!canRegister()) {
    		return false;
    	}
        plugin = (Main) Bukkit.getPluginManager().getPlugin(getPlugin());
        if (plugin == null) {
            return false;
        }
        return PlaceholderAPI.registerPlaceholderHook(getIdentifier(), this);
    }
    
    public String getAuthor() {
        return "BrowkTQ";
    }
    
    public String getIdentifier() {
        return "qcrates";
    }
    
    public String getPlugin() {
        return "qCrates";
    }
    
    public String getVersion() {
        return "1.0.0";
    }
    
    public String onPlaceholderRequest(final Player p, final String identifier) {
        if (this.plugin == null || p == null) {
            return "";
        }
        switch (identifier) {
            case "souls": {
                return this.plugin.getSouls(p);
            }
            default:
                break;
        }
        return null;
    }
    
    public void clear() {
        this.plugin = null;
    }
}
