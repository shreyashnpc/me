'use client'

import Link from 'next/link'
import { useState, useEffect } from 'react'
import { 
  HiHome, 
  HiUser, 
  HiFolder, 
  HiEnvelope, 
  HiBriefcase
} from 'react-icons/hi2'
import { 
  FiGithub, 
  FiLinkedin, 
  FiTwitter, 
  FiInstagram 
} from 'react-icons/fi'
import type { IconType } from 'react-icons'
import './Navbar.css'

export default function Navbar() {
  const [isScrolled, setIsScrolled] = useState(false)
  const [isMobileMenuOpen, setIsMobileMenuOpen] = useState(false)

  useEffect(() => {
    const handleScroll = () => {
      setIsScrolled(window.scrollY > 50)
    }
    window.addEventListener('scroll', handleScroll)
    return () => window.removeEventListener('scroll', handleScroll)
  }, [])

  const navLinks: Array<{ href: string; icon: IconType; label: string }> = [
    { href: '/', icon: HiHome, label: 'Home' },
    { href: '/about', icon: HiUser, label: 'About' },
    { href: '/projects', icon: HiFolder, label: 'Projects' },
    { href: '/contact', icon: HiEnvelope, label: 'Contact' },
    { href: '/experience', icon: HiBriefcase, label: 'Experience' },
  ]

  const socialLinks: Array<{ href: string; icon: IconType; label: string }> = [
    { href: 'https://github.com/shreyashnpc', icon: FiGithub, label: 'GitHub' },
    { href: 'https://linkedin.com', icon: FiLinkedin, label: 'LinkedIn' },
    { href: 'https://twitter.com', icon: FiTwitter, label: 'Twitter' },
    { href: 'https://instagram.com', icon: FiInstagram, label: 'Instagram' },
  ]

  return (
    <nav className={`navbar ${isScrolled ? 'scrolled' : ''}`}>
      <div className="navbar-container">
        {/* Mac Traffic Light Buttons */}
        <div className="traffic-lights">
          <div className="traffic-light traffic-light-red"></div>
          <div className="traffic-light traffic-light-yellow"></div>
          <div className="traffic-light traffic-light-green"></div>
        </div>

        {/* Left Side - Navigation Links */}
        <ul className="navbar-menu-left">
          {navLinks.map((link, index) => {
            const IconComponent = link.icon
            return (
              <li key={link.href} style={{ animationDelay: `${index * 0.1}s` }}>
                <Link
                  href={link.href}
                  className="navbar-link"
                  title={link.label}
                >
                  <IconComponent className="link-icon" />
                </Link>
              </li>
            )
          })}
        </ul>

        {/* Center - Name */}
        <div className="navbar-center">
          <Link href="/" className="navbar-logo">
            <div className="logo-container">
              <div className="logo-text">
                <span className="name-first">SHREYASH</span>
                <span className="name-last">PANDEY</span>
              </div>
              <div className="logo-rings">
                <span className="ring ring-1"></span>
                <span className="ring ring-2"></span>
                <span className="ring ring-3"></span>
              </div>
            </div>
          </Link>
        </div>

        {/* Right Side - Social Media Icons */}
        <div className="navbar-social">
          {socialLinks.map((social, index) => {
            const IconComponent = social.icon
            return (
              <a
                key={social.label}
                href={social.href}
                target="_blank"
                rel="noopener noreferrer"
                className="social-icon"
                aria-label={social.label}
                title={social.label}
                style={{ animationDelay: `${(navLinks.length + index) * 0.1}s` }}
              >
                <IconComponent className="social-icon-svg" />
              </a>
            )
          })}
        </div>

        {/* Mobile Menu Toggle */}
        <button
          className="mobile-menu-toggle"
          onClick={() => setIsMobileMenuOpen(!isMobileMenuOpen)}
          aria-label="Toggle menu"
        >
          <span></span>
          <span></span>
          <span></span>
        </button>
      </div>

      {/* Mobile Menu */}
      <div className={`mobile-menu ${isMobileMenuOpen ? 'active' : ''}`}>
        <ul className="mobile-menu-list">
          {navLinks.map((link) => (
            <li key={link.href}>
              <Link
                href={link.href}
                onClick={() => setIsMobileMenuOpen(false)}
                className="mobile-link"
              >
                {link.label}
              </Link>
            </li>
          ))}
        </ul>
        <div className="mobile-social">
          {socialLinks.map((social) => {
            const IconComponent = social.icon
            return (
              <a
                key={social.label}
                href={social.href}
                target="_blank"
                rel="noopener noreferrer"
                className="mobile-social-icon"
                aria-label={social.label}
              >
                <IconComponent className="mobile-social-svg" />
              </a>
            )
          })}
        </div>
      </div>
    </nav>
  )
}

